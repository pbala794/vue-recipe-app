<template>
    <div>
        <button type="button" class="filter-btn"
                @click="toggleFilters">
            Filters <i class="fas fa-filter"></i>
        </button>

        <!-- <div class="filters">
            <select>
                <option>Category 1</option>
                <option>Category 2</option>
                <option>Category 3</option>
            </select>

            <select>
                <option>Category 1</option>
                <option>Category 2</option>
                <option>Category 3</option>
            </select>

            <select>
                <option>Category 1</option>
                <option>Category 2</option>
                <option>Category 3</option>
            </select>
        </div> -->
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
        padding: 10px;
        border-radius: 2px;
        font-size: 1.2rem;
        letter-spacing: .8px;
        margin: 0 5px;
        color: #3d3d3d;
        transition: all .2s ease-in-out;
        text-transform: uppercase;
    }

    .filter-btn:hover {
        color: #fff;
        background: #c776306e;
    }

</style>

