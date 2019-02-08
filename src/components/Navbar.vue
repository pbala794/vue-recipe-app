<template>
    <div class="wrapper">
        <nav class="top-bar">
            <div class="menu-icon"
                @click="onMenuClick"
                :class="{ 'menu-icon-active': sidebarIsActive }">
                <i class="fas fa-bars"></i>
            </div>

            <ul class="navbar" :class="{ 'navbar-active': sidebarIsActive }">
                <li class="menu-item">Home</li>
                <li class="menu-item">About</li>
                <li class="menu-item">Contact</li>
            </ul>

            <div class="overlay"></div>

            <div class="search">
                <SearchBar></SearchBar>
            </div>
        </nav>

        <div class="filter-bar">
            <RecipeFilter></RecipeFilter>
            <Favourites></Favourites>
        </div>
  </div>
</template>

<script>
import SearchBar from './SearchBar'
import RecipeFilter from './RecipeFilter'
import Favourites from './Favourites'

export default {
  name: 'navbar',
  components: {
    SearchBar,
    RecipeFilter,
    Favourites
  },
  data() {
    return {
        sidebarIsActive: false,
    }
  },
  methods: {
      onMenuClick() {
          this.sidebarIsActive = !this.sidebarIsActive;
      }
  }
}
</script>

<style scoped>

.wrapper {
    position: relative;
}

.top-bar {
    display: flex;
    background: #fded8c;
    align-items: center;
    height: 70px;
    position: fixed;
    top: 0;
    left: 0;
    right: 0;
    z-index: 20;
    border-bottom: 4px solid #d1bf55;
}

.menu-icon {
    font-size: 2.1rem;
    padding: 5px 25px;
    cursor: pointer;
    transition: color .5s ease-in-out;
}

.menu-icon-active {
    color: #beb15e;
}

.navbar {
    position: fixed;
    z-index: 10;
    font-size: 3rem;
    display: flex;
    flex-direction: column;
    justify-content: center;
    left: 0;
    top: -100%;
    height: 100%;
    background: inherit;
    width: 100%;
    transition: all .5s ease-in-out;
}

.navbar-active {
    top: 74px;
}

.menu-item {
    padding: 8px;
    cursor: pointer;
}

.menu-item:first-child {
    padding-top: 25px;
}

.menu-item:hover {
    border-bottom: 3px solid #333;
    transition: all .1s linear;
}

.search {
    width: 100%;
}

.filter-bar {
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
}

@media all and (min-width: 768px) {
    
    .navbar {
        position: fixed;
        z-index: 10;
        display: flex;
        flex-direction: column;
        justify-content: flex-start;
        left: -150px;
        top: 74px;
        background: inherit;
        width: 150px;
        height: 100%;
        font-size: 1.5rem;
        transition: all .5s ease-in-out;
    }

    .navbar-active {
        left: 0;
    }
}

</style>
