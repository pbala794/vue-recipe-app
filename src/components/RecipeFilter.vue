<template>
    <div>
        <button type="button" class="filter-btn"
                @click="toggleFilters">
            Show filters
        </button>
    </div>
</template>

<script>
export default {
    name: "RecipeFilter",
    data() {
        return {
            isFiltersVisible: false    
        }
    },
    methods: {
        toggleFilters() {
            this.isFiltersVisible = !this.isFiltersVisible;
        }
    }
}
</script>

<style scoped>

    .filter-btn {
        background: #ffb16b6e;
        border: none;
        padding: 7px;
        border-radius: 2px;
        font-size: 1.2rem;
    }

</style>

