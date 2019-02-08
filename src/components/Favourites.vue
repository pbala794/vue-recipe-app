<template>
    <div>
        <button type="button" class="favourites-btn"
                @click="toggleFavourites">
            Favourites <i class="far fa-heart"></i>
        </button>
    </div>
</template>

<script>
export default {
    name: 'Favourites',
    methods: {
        toggleFavourites() {
            
        }
    }
}
</script>

<style scoped>

    .favourites-btn {
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

    .favourites-btn:hover {
        color: #fff;
        background: #c776306e;
    }

</style>


