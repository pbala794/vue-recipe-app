<template>
  <div id="app">
    <link rel="stylesheet" 
        href="https://use.fontawesome.com/releases/v5.2.0/css/all.css" 
        integrity="sha384-hWVjflwFxL6sNzntih27bfxkr27PmbbK/iSvJ+a4+0owXq79v+lsFkW54bOGbiDQ" 
        crossorigin="anonymous">
        
    <header>
      <Navbar></Navbar>

      <div class="options-bar">
        <RecipeFilter></RecipeFilter>
        <Favourites></Favourites>
        </div>
    </header>

    <div class="content">
      <div class="loader" v-if="!isLoaded">
        <i class="fas fa-spin fa-spinner"></i>
      </div>

      <div class="no-results" v-if="isLoaded && !(recipies && recipies.length > 0)">
        <h2>No search results. Try another recipe.</h2>
      </div>

      <div class="recipies-list" v-if="isLoaded && recipies && recipies.length > 0">
        <RecipeBox v-for="recipe in recipies" :key="recipe.idMeal"
                   v-bind:recipe="recipe">
        </RecipeBox>
      </div>
    </div>

  </div>
</template>

<script>
import axios from 'axios';
import { EventBus } from './event-bus.js'

import Navbar from './components/Navbar.vue'
import RecipeFilter from './components/RecipeFilter'
import Favourites from './components/Favourites'
import RecipeBox from './components/RecipeBox'

export default {
  name: 'app',
  data() {
    return {
      isMobile: true,
      recipies: [],
      isLoaded: false
    }
  },
  components: {
    Navbar,
    RecipeFilter,
    Favourites,
    RecipeBox
  },
  // created() {
  //   if (this.getBrowserWidth() > 768) {
  //     this.isMobile = false;
  //   }
  // },
  mounted() {
    axios.get('https://www.themealdb.com/api/json/v1/1/latest.php')
      .then(response => {
          this.recipies = response.data.meals;
          EventBus.$emit('latest', this.recipies);
          this.isLoaded = true;
      })
      .catch(error => console.log(error))

      EventBus.$on('loading', () => this.isLoaded = false);
      EventBus.$on('search', recipies => {
        this.recipies = recipies;
        this.isLoaded = true;
      });
      EventBus.$on('filter', filters => {
        this.onRecipeFilter(filters);
      });
      // window.addEventListener('resize', () => {
      //   this.getBrowserWidth() > 768 ? this.isMobile = false : this.isMobile = false;
      //   console.log(this.isMobile);
      // });
  },
  methods: {
    getBrowserWidth() {
      return Math.max(
        document.body.scrollWidth,
        document.documentElement.scrollWidth,
        document.body.offsetWidth,
        document.documentElement.offsetWidth,
        document.documentElement.clientWidth
      )
    },
    onRecipeFilter(filtersObj) {
      let areaFiltered = [],
          catFiltered = [],
          tagsFiltered = [];

      if (filtersObj['areaFilters'].length > 0) {
        areaFiltered = this.recipies.filter(recipe => {
          return filtersObj['areaFilters'].includes(recipe.strArea);
        })
      }
      if (filtersObj['catFilters'].length > 0) {
        catFiltered = this.recipies.filter(recipe => {
          return filtersObj['catFilters'].includes(recipe.strCategory);
        })
      }
      if (filtersObj['tagFilters'].length > 0) {
        tagsFiltered = this.recipies.filter(recipe => {
          return filtersObj['strTags'].includes(recipe.strTags);
        })
      }

      this.recipies = [...areaFiltered, ...catFiltered, ...tagsFiltered];
      // console.log(this.recipies, filtersObj);
      // console.log(this.recipies, filtersObj);
      // console.log(this.recipies, filtersObj);
    }
  },
  destroyed() {
    EventBus.$off();
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
  min-height: 100vh;
}

.loader {
  margin: 0 auto;
  align-self: center;
  font-size: 8rem;
}

.no-results {
  align-self: center;
  margin: 0 auto;
  font-size: 1.2rem;
  border: 4px solid #fded8c;
  padding: 10px;
}

.options-bar {
  display: flex;
  justify-content: center;
  align-items: center;
  position: fixed;
  top: 74px;
  left: 0;
  right: 0;
  background: #fded8c;
  padding: 15px;
  min-height: 20px;
  z-index: 2;
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
