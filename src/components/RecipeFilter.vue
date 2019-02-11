<template>
    <div>
        <button type="button" class="filter-btn"
                :class="{'filter-btn-active': isFiltersVisible}"
                @click="toggleFilters">
            Filters <i class="fas fa-filter"></i>
        </button>

        <div class="filters" v-if="isFiltersVisible">
            <h2 class="filter-title">Category</h2>
            <div class="filter-list">
                <span class="filter-list-item" 
                      v-for="cat of availableFilters.catFilters" :key="cat"
                      @click="activateFilter('cat', cat)"
                      :class="{'filter-item-active': filterIsActive}">
                    {{ cat }}
                </span>
                <span v-if="!availableFilters.catFilters.length > 0">
                    No available category filters
                </span>
            </div>

            <h2 class="filter-title">Area</h2>
            <div class="filter-list">
                <span class="filter-list-item" 
                      v-for="area of availableFilters.areaFilters" :key="area"
                      @click="activateFilter('area', area)"
                      :class="{'filter-item-active': filterIsActive}">
                    {{ area }}
                </span>
                <span v-if="!availableFilters.areaFilters.length > 0">
                    No available area filters
                </span>
            </div>

            <h2 class="filter-title">Tags</h2>
            <div class="filter-list">
                <span class="filter-list-item" 
                      v-for="tag of availableFilters.tagFilters" :key="tag"
                      @click="activateFilter('tag', tag)"
                      :class="{'filter-item-active': filterIsActive}">
                    {{ tag }}
                </span>
                <span v-if="!availableFilters.tagFilters.length > 0">
                    No available tag filters
                </span>
            </div>
        </div>
    </div>
</template>

<script>
import { EventBus } from '../event-bus.js'

export default {
    name: "RecipeFilter",
    data() {
        return {
            recipies: [],
            availableFilters: {
                catFilters: [],
                areaFilters: [],
                tagFilters: []
            },
            activeFilters: {
                catFilters: [],
                areaFilters: [],
                tagFilters: []                
            },
            isFiltersVisible: false,
            filterIsActive: false    
        }
    },
    mounted() {
        EventBus.$on('latest', recipies => {
            this.recipies = recipies;
            this.getFilters();
        })

        EventBus.$on('search', recipies => {
            this.recipies = recipies;
            this.getFilters();
        })
    },
    methods: {
        toggleFilters() {
            this.isFiltersVisible = !this.isFiltersVisible;
        },
        getFilters() {
            if (this.recipies && this.recipies.length > 0) {
                this.recipies.forEach(recipe => {
                    if (!(this.availableFilters.catFilters.indexOf(recipe.strCategory) > -1) && recipe.strCategory) {
                        this.availableFilters.catFilters.push(recipe.strCategory);
                    }
                    if (!(this.availableFilters.areaFilters.indexOf(recipe.strArea) > -1) && recipe.strArea) {
                        this.availableFilters.areaFilters.push(recipe.strArea);
                    }
                    if (!(this.availableFilters.tagFilters.indexOf(recipe.strTags) > -1) && recipe.strTags) {
                        this.availableFilters.tagFilters.push(recipe.strTags);
                    }
                });
            } else {
                this.availableFilters.catFilters = [];
                this.availableFilters.areaFilters = [];
                this.availableFilters.tagFilters = [];
            }
        },
        // available filterTypes - 'cat' , 'area', 'tag 
        activateFilter(filterType, activeFilter) {
            const types = {
                'cat': () => {
                    if (!(this.activeFilters.catFilters.indexOf(activeFilter) > -1)) {
                        this.activeFilters.catFilters.push(activeFilter);
                    }
                },
                'area': () => {
                    if (!(this.activeFilters.areaFilters.indexOf(activeFilter) > -1)) {
                        this.activeFilters.areaFilters.push(activeFilter);
                    }
                },
                'tag': () => {
                    if (!(this.activeFilters.tagFilters.indexOf(activeFilter) > -1)) {
                        this.activeFilters.tagFilters.push(activeFilter) 
                    }
                }
            };
            types[filterType]();
            EventBus.$emit('filter', this.activeFilters);
        }
    }
}
</script>

<style scoped>

    .filter-btn {
        background: #ffb16b6e;
        border: none;
        padding: 10px;
        border-radius: 2px;
        font-size: 1.2rem;
        letter-spacing: .8px;
        margin: 0 5px;
        color: #3d3d3d;
        transition: all .2s ease-in-out;
        text-transform: uppercase;
    }

    .filter-btn:hover,
    .filter-btn-active {
        color: #fff;
        background: #c776306e;
    }

    .filters {
        position: absolute;
        left: 0;
        top: 72px;
        width: 100%;
        min-height: 100vh;
        background: rgba(253, 237, 140, .9);
        justify-content: center;
    }

    .filter-title {
        font-size: 1.5rem;
        text-align: left;
        margin: 15px;
    }

    .filter-list {
        display: flex;
        flex-wrap: wrap;
        border: 2px solid #ddd;
        padding: 10px;
        min-height: 100px;
        width: 80%;
        background: rgba(0, 0, 0, .1);
        margin: 0 auto;
    }

    .filter-list-item {
        border: 1px solid rgb(3, 3, 66);
        padding: 5px 10px;
        height: 30px;
        line-height: 30px;
        margin: 5px;
        cursor: pointer;
        transition: all .2s ease-in-out;
    }

    .filter-list-item:hover, 
    .filter-item-active {
        background: rgba(0, 0, 0, .5);
        color: #fff;
    }

</style>

