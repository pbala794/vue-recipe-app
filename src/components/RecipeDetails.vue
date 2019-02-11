<template>
    <div class="recipe-details">
        <div class="details-col">
            <iframe width="100%" height="315" :src="ytUrlRemainder" 
                    frameborder="0" 
                    allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture">
            </iframe>
        </div>
        <div class="details-col">
            <h2 class="details-title">Instruction</h2>
            <p class="details-text">{{ recipe.strInstructions }}</p>

            <h2 class="details-title">Ingredients + Measure</h2>
            <ul>
                <li v-for="num in ingredientsNum" :key="num" class="details-text">
                    {{ recipe['strIngredient' + num] ? recipe['strIngredient' + num]  + ' -' : '' }} 
                    {{ recipe['strMeasure' + num] ? recipe['strMeasure' + num] : '' }}
                </li>
            </ul>
        </div>
    </div>
</template>

<script>
export default {
    name: 'RecipeDetails',
    props: {
        recipe: {
            type: Object,
            required: true
        }
    },
    data() {
        return {
            ingredientsNum: [1,2,3,4,5,6,7,8,9,10,11,12,13,14,15,16,17,18,19,20],
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
}
</script>

<style scoped>

.details-col {
    width: 100%;
} 

.details-title {
    text-align: left;
    font-size: 1.4rem;
    margin: 15px 0;
}

.details-text {
    font-size: 1rem;
    line-height: 1.2rem;
    text-align: justify;
    letter-spacing: .5px;
}

.recipe-details {
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    border-top: 3px solid lightgrey;
    padding: 10px;
    width: 100%;
    min-height: 340px;
    box-sizing: border-box;
    /* margin: 15px;
    border: 3px solid lightgrey;
    border-radius: 5px; */
}

@media all and (min-width: 768px) {
    .recipe-details {
        flex-direction: row;
        margin-bottom: 25px;
        width: 100%;
    }

    .details-col:first-child {
        flex: 1; 
    }

    .details-col:nth-child(2) {
        flex: 2; 
        padding: 15px;
    }


}

</style>
