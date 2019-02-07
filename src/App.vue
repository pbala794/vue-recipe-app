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
      <div class="filters"></div>

      <div class="recipies-list">
        <RecipeBox v-for="recipe in recipies" :key="recipe.idMeal" 
                  v-bind:recipe="recipe"></RecipeBox>
      </div>  
    </div>

  </div>
</template>

<script>
import axios from 'axios';

import Navbar from './components/Navbar.vue'
import RecipeBox from './components/RecipeBox'

export default {
  name: 'app',
  data() {
    return {
      recipies: []
    }
  },
  components: {
    Navbar,
    RecipeBox
  },
  mounted() {
    axios.get('https://www.themealdb.com/api/json/v1/1/latest.php')
      .then(response => {
          this.recipies = response.data.meals;
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

.filters {
  width: 200px;
  height: 100vh;
  background: gainsboro;
}

.recipies-list {
  display: flex;
  flex-wrap: wrap;
  justify-content: space-around;
}

</style>
