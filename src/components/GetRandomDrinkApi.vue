<template>
    <!--<a class="prev" onclick="plusSlides(-1)">&#10094;</a>-->
    <div class="slides">
        <drinksKomponent v-for="(drink, index) in posts.drinks" :key="index" 
                :drinkName="drink.strDrink"
                :drinkCategory="drink.strCategory"
                :drinkIngredients="ingredients"
                :drinksImg="drink.strDrinkThumb"/>
        <a class="next" @click="getRandomCocktail()">&#10095;</a>         
    </div>
</template>

<script>
import drinksKomponent from './drinks.vue';

  export default {
      name: 'GetRandomDrinkApi',
      components: { drinksKomponent },
      data() {
        return {
            posts: [],
            ingredients: [],
            drink: []
        }
      },
      // created är en funktion som kallas när sidan laddas
      // created hämtar en random cocktail
      created(){
        // Tom array som vi ska lägga objektet i
        const ingredientsPosts = [];
        fetch('https://www.thecocktaildb.com/api/json/v1/1/random.php')
        .then(response => response.json())
        .then(json => {
            //console.log(json)
            this.posts = json
            // Objektet som hämtas från api:et med poistion 0 läggs i variablen filtredDrinks
            const filtredDrinks = json.drinks[0]
            // Loopar objektet, för varje property som finns i objektet filtredDrinks
            for (const property in filtredDrinks) {
                // om nyckeln (property) innehåller strIngredient och värdet inte är null så pushas värdet in i arrayen ingeredientsPosts
                if ( property.includes("strIngredient") && filtredDrinks[property] !== null) {
                    ingredientsPosts.push(`${filtredDrinks[property]}`);
                    this.ingredients = ingredientsPosts;
                }  
            }
        }
        );   
    }
    ,
    methods: {
        getRandomCocktail() {
            const ingredientsPosts = [];
            fetch('https://www.thecocktaildb.com/api/json/v1/1/random.php')
            .then((response) => response.json())
            .then((json) => {
                console.log(json)
                this.posts = json
                const filtredDrinks = json.drinks[0]
            // Loopar objektet, för varje property som finns i objektet filtredDrinks
            for (const property in filtredDrinks) {
                // om nyckeln (property) innehåller strIngredient och värdet inte är null så pushas värdet in i arrayen ingeredientsPosts
                if ( property.includes("strIngredient") && filtredDrinks[property] !== null) {
                    ingredientsPosts.push(`${filtredDrinks[property]}`);
                    this.ingredients = ingredientsPosts;
                }  
            }
            });
        }
    }
  }
</script>

<style>
    .slides {
        display: flex;
        justify-content: space-around;
        align-items: center;
        margin: 3% 0% 3% 0%;
        min-height: 80vh;
    }
    .slides .drinks {
        justify-content: space-around;
    }

    .next {
        font-size: 2.2em;
        cursor: pointer;
        color: #cf8205;
        transition: 0.6s ease;
    }
    .next:hover {
        color: rgb(255, 215, 155);
    }

    @media screen and (max-width: 1024px) {
        .slides img {
            max-width: 60%;
        }
    }
    @media only screen and (max-width: 768px) {
        .slides {
            flex-direction: column;
            justify-content: center;
        }
        .next {
            background-image: radial-gradient(circle, rgb(29, 29, 29), black);
            width: 100%;
            margin-top: 4%;
            border-radius: 20px;
            box-shadow: 1px 0px 8px 0px rgba(0, 0, 0, 0.589);
        }
    }
</style>