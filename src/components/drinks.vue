<template>
    <div class="drinks">
        <img :src="drinksImg" class="drink-img">            
        <div class="drinkText">
            <h2>{{ drinkName }}</h2>
            <h2>{{ drinkCategory }}</h2>
            <ul>
                <li v-for="(filter, index) in drinkIngredients " :key="index">{{ filter }}</li>
            </ul>
        </div>

    </div>
</template>

<script>

    export default {
        name: 'drinksKomponent',
        props: {
            drinkName: String,
            drinkCategory: String,
            drinkIngredients: Array,
            drinksImg: String
        }
    }
</script>

<style scoped>
    .drinks {
        display: flex;
        justify-content: space-around;
        font-size: 1.4em;
    }

    .drink-img {
        max-width: 100%;
        height: auto;
    }
    .drinkText {
        display: flex;
        flex-direction: column;
        font-family: 'Shadows Into Light Two', cursive;
        align-self: center;
        animation-name: fade;
        animation-duration: 3s;
    }

    @keyframes fade {
    0%   {opacity: 0%;}
    100% {opacity: 100%;}
    }
    @media screen and (max-width: 1024px) {
        .drink-img {
            max-width: 60%;
        }
    }
</style>