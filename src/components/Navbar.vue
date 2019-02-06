<template>
    <div>
        <nav class="top-bar">
            <div class="menu-icon"
                @click="onMenuClick"
                :class="{ 'menu-icon-active': sidebarIsActive }">
                <i class="fas fa-bars"></i>
            </div>

            <SearchBar></SearchBar>

            <ul class="navbar" :class="{ 'navbar-active': sidebarIsActive }">
                <li class="menu-item">Home</li>
                <li class="menu-item">About</li>
                <li class="menu-item">Contact</li>
            </ul>
        </nav>
  </div>
</template>

<script>
import SearchBar from './SearchBar'

export default {
  name: 'navbar',
  components: {
    SearchBar
  },
  data() {
    return {
        sidebarIsActive: true,
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

.top-bar {
    display: flex;
    background: #fded8c;
    align-items: center;
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
    display: flex;
    flex-direction: column;
    left: -150px;
    top: 42px;
    background: inherit;
    width: 150px;
    height: 100%;
    transition: all .5s ease-in-out;
}

.navbar-active {
    left: 0;
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
    /* background: #ffea6b; */
}

</style>
