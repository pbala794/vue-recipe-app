<template>
  <div id="app">
    <link rel="stylesheet" 
        href="https://use.fontawesome.com/releases/v5.2.0/css/all.css" 
        integrity="sha384-hWVjflwFxL6sNzntih27bfxkr27PmbbK/iSvJ+a4+0owXq79v+lsFkW54bOGbiDQ" 
        crossorigin="anonymous">
        
    <header>
      <Navbar></Navbar>
    </header>

    <div class="content">
      <!-- <div class="filters"></div> -->
  
      <div class="loader" v-if="!isLoaded">
        <i class="fas fa-spin fa-spinner"></i>
      </div>

      <div class="recipies-list" v-if="isLoaded">
        <RecipeBox v-for="recipe in recipies" :key="recipe.idMeal" 
                  v-bind:recipe="recipe">
        </RecipeBox>
        <RecipeDetails v-if="showDetails" :recipe="selectedRecipe"></RecipeDetails>
      </div>
    </div>

  </div>
</template>

<script>
import axios from 'axios';
import { EventBus } from './event-bus.js'

import Navbar from './components/Navbar.vue'
import RecipeBox from './components/RecipeBox'
import RecipeDetails from './components/RecipeDetails'

export default {
  name: 'app',
  data() {
    return {
      selectedRecipe: {},
      recipies: [],
      isLoaded: false,
      showDetails: false
    }
  },
  components: {
    Navbar,
    RecipeBox,
    RecipeDetails
  },
  mounted() {
    axios.get('https://www.themealdb.com/api/json/v1/1/latest.php')
      .then(response => {
          this.recipies = response.data.meals;
          this.isLoaded = true;
      })
      .catch(error => console.log(error))

      EventBus.$on('search', recipies => {
        this.recipies = recipies;
      });

      EventBus.$on('show-details', (status, recipe) => {
        this.selectedRecipe = recipe;
        this.showDetails = status;
      });
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

.content {
  display: flex;
}

.loader {
  margin: 0 auto;
  align-self: center;
  font-size: 8rem;
}

.filters {
  width: 200px;
  height: 100vh;
  background: gainsboro;
}

.recipies-list {
  margin-top: 150px;
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
}

@media all and (min-width: 768px) {

}

</style>
