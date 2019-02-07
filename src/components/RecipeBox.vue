<template>
    <div class="recipe-box">
        <img :src="recipe.strSource" alt="meal">
        <p>{{ recipe.strMeal }}</p>
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
    height: 300px;
    background: aquamarine;
    margin: 15px;
}

</style>


