<template>
    <div class="recipe-box">
        <div class="img-wrapper">
            <img :src="recipe.strMealThumb" class="recipe-thumb" alt="meal">
        </div>
        <p class="recipe-title">{{ recipe.strMeal }}</p>
    </div>
</template>

<script>
export default {
    name: 'RecipeBox',
    props: {
        recipe: {
            type: Object,
            required: true
        }
    }
}
</script>

<style scoped>

.recipe-box {
    width: 420px;
    height: 340px;
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

</style>


