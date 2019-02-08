<template>
    <div class="recipe-box">
        <div class="img-wrapper" @click="showRecipe(recipe)">
            <img :src="recipe.strMealThumb" class="recipe-thumb" alt="meal">
        </div>

        <p class="recipe-title">{{ recipe.strMeal }}</p>
    </div>
</template>

<script>
import { EventBus } from '../event-bus.js'

export default {
    name: 'RecipeBox',
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
        showRecipe(recipe) {
            this.showRecipeDetails = true;
            EventBus.$emit('show-details', this.showRecipeDetails, this.recipe);
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
    height: 280px;
}

.recipe-thumb {
    width: 100%;
    height: 100%;
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


