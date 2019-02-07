<template>
    <div class="search-wrapper">
        <!-- <span class="search-icon">
            <i class="fas fa-search"></i>
        </span> -->
        <input type="text" class="search" placeholder="Search for recipe...">
    </div>
</template>

<script>
export default {
    name: 'SearchBar',
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

