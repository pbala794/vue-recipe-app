<template>
    <div class="search-wrapper">
        <form @submit.prevent="onSearch">
            <input type="text" class="search" placeholder="Search for recipe..."
                    v-model="searchValue">
        </form>
    </div>
</template>

<script>
import axios from 'axios'
import { EventBus } from '../event-bus.js'

export default {
    name: 'SearchBar',
    data() {
        return {
            searchValue: ''
        }
    },
    methods: {
        onSearch() {
            EventBus.$emit('loading');
            
            axios.get(`https://www.themealdb.com/api/json/v1/1/search.php?s=${this.searchValue}`)
                .then(results => {
                    this.searchValue = '';
                    EventBus.$emit('search', results.data.meals);
                })
                .catch(error => console.log(error));
        }
    }
}
</script>

<style scoped>

    .search {
        height: 25px;
        width: 300px;
        padding: 5px;
        background: transparent;
        position: relative;
    }

    .search-icon {
        position: absolute;
        left: 0;
    }

    @media all and (min-width: 768px) {
        .search {
            width: 500px;
        }
    }

</style>

