<template>
    <div class="recipe-box">
        <div class="img-wrapper" @click="toggleRecipe">
            <span class="thumb-text">
                {{ !showRecipeDetails ? 'show details' : 'hide details' }}
            </span>
            <img :src="recipe.strMealThumb" class="recipe-thumb" alt="meal">
        </div>

        <p class="recipe-title">{{ recipe.strMeal }}</p>

        <RecipeDetails v-if="showRecipeDetails" :recipe="recipe"></RecipeDetails>
    </div>
</template>

<script>
import { EventBus } from '../event-bus.js'
import RecipeDetails from './RecipeDetails';

export default {
    name: 'RecipeBox',
    components: {
        RecipeDetails
    },
    props: {
        recipe: {
            type: Object,
            required: true
        }
    },
    data() {
        return {
            ingredientsNum: [1,2,3,4,5,6,7,8,9,10,11,12,13,14,15,16,17,18,19,20],
            showRecipeDetails: false
        }
    },
    computed: {
        ytUrlRemainder() {
            const ytBaseUrl = 'https://www.youtube.com/embed/';
            const videoUrl = this.recipe.strYoutube;
            const urlEnd = videoUrl.split('=')[1];
            return `${ytBaseUrl}${urlEnd}`;
        }
    },
    methods: {
        toggleRecipe() {
            this.showRecipeDetails = !this.showRecipeDetails;
        }
    }
}
</script>

<style scoped>

.recipe-box {
    width: 100%;
    min-height: 340px;
    margin: 15px;
    border: 3px solid lightgrey;
    border-radius: 5px;
}

.img-wrapper {
    position: relative;
    display: flex;
    justify-content: center;
    align-items: center;
    height: 280px;
    background: #000;
}

.img-wrapper:hover img {
    cursor: pointer;
    opacity: .5;
}

.recipe-thumb {
    width: 100%;
    height: 100%;
    opacity: 1;
    transition: opacity .15s ease-in-out;
    z-index: 1;
}

.thumb-text {
    position: absolute;
    font-size: 1.5rem;
    text-transform: uppercase;
    color: #fff;
}

.recipe-title {
    font-size: 1.1rem;
    text-transform: uppercase;
    line-height: 60px;
}

@media all and (min-width: 768px) {
    .recipe-box {
        width: 460px;
    }
}

</style>


