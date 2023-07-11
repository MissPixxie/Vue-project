<template>
    <h1 class="title">{{ $route.params.strCategory }}</h1>
    <div class="category-container">
      <div v-show="!mobile">
        <h3>Drinks</h3>
        <div class="list">
                <div v-for="(list, index) in listinCategory.drinks" :key="index" class="listOfDrinks"> 
                    <a @click="getDrink(list.strDrink)"> {{ list.strDrink }} </a>
                </div>
        </div>       
      </div>
        <div v-show="mobile">
            <div class="list">
                <div v-if="isOpen">
                    <a @click="isOpen = !isOpen" v-show="mobile" class="list-title">&#10094; Drinks</a>
                </div>
                <div v-else>
                    <a @click="isOpen = !isOpen" v-show="mobile" class="list-title">Drinks</a>
                </div>
                <transition name="mobile-nav" appear>
                    <div v-if="isOpen" class="dropdown-nav">
                            <ul>
                                <li v-for="(list, index) in listinCategory.drinks" :key="index">
                                    <a @click="isMobileOpen = !isMobileOpen && getDrink(list.strDrink)">{{ list.strDrink }}</a>
                                </li>
                            </ul>
                    </div>
                </transition>
            </div>

        </div>
        <div class="container">
            <drinksKomponent v-for="(drinkInList, index) in drink.drinks" :key="index" 
            :drinkName="drinkInList.strDrink"
            :drinkCategory="drinkInList.strCategory"
            :drinkIngredients="ingredients"
            :drinksImg="drinkInList.strDrinkThumb"/>
        </div> 
    </div>
</template>
<script>

import drinksKomponent from './drinks.vue'

  export default {
      name: 'GetCategoryApi',
      components: { drinksKomponent },
      data() {
        return {
            posts: [],
            listinCategory: [],
            drink: [],
            ingredients: [],
            mobile: null,
            mobileNav: null,
            windowWidth: null,
            isOpen: false,
            isMobileOpen: false,
        }
      },
      beforeCreate() {
        for ( const values in this.$route.params ) {
            console.log(this.$route.params[values])
            let category = this.$route.params[values]
            fetch(`https://www.thecocktaildb.com/api/json/v1/1/filter.php?c=${category}`)
                      .then((response) => response.json())
                      .then((json) => {
                      //console.log(json)
                      this.listinCategory = json
                      });
        }
        // kontrollerar när man klickar på en ny kategori
        this.$watch( () => this.$route.params, (toParams) => {
            for (const values in toParams) {
                //console.log(toParams[values])
                let kategori = toParams[values];
                if (toParams[values].includes(" ")) {
                    // Tar bort mellanslag och ersätter med _ för att kunna söka i api:et
                    let ny = kategori.replace(/ /g, "_");
                      //console.log(ny)
                      fetch(`https://www.thecocktaildb.com/api/json/v1/1/filter.php?c=${ny}`)
                      .then((response) => response.json())
                      .then((json) => {
                      //console.log(json)
                      this.listinCategory = json
                      });
                }
                else {
                    fetch(`https://www.thecocktaildb.com/api/json/v1/1/filter.php?c=${kategori}`)
                      .then((response) => response.json())
                      .then((json) => {
                      //console.log(json)
                      this.listinCategory = json
                      });
                }
            }
            //console.log(toParams);
            //console.log(this.$route.params); 
        })
      },
      created(){
        window.addEventListener('resize', this.checkScreen);
        this.checkScreen();
    },
    methods: {
          getDrink (drinkName){
            this.isOpen = !this.isOpen;
            const ingredientsPosts = [];
            fetch(`https://www.thecocktaildb.com/api/json/v1/1/search.php?s=${drinkName}`)
            .then((response) => response.json())
            .then((json) => {
                //console.log(json)
                this.drink = json
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
          },
        toggleMobileNav() {
        this.mobileNav = !this.mobileNav;
        },
        checkScreen() {
            this.windowWidth = window.innerWidth;
            if (this.windowWidth <= 750) {
                this.mobile = true;
                return;
            }
            else {
                this.mobile = false;
                this.mobileNav = false;
            return;          
            }
        }         
    },
  }
</script>

<style>

    .title {
        font-size: 2.7em;
    }
    .category-container {
        display: flex;
        flex-direction: column;
        justify-content: space-around;
        align-items: center;
        margin-bottom: 3%;
        min-height: 51vh;
    }
    .category-container h3 {
        font-size: 1.9em;
    }
    .listOfDrinks {
        background: linear-gradient(to right, rgba(34, 34, 34, 0.158), rgba(58, 58, 58, 0.322));
        padding: 0.4%;
        margin: 0.4%;
        transition: background-color 0.5s;
        box-shadow: 0 4px 3px 0 rgba(241, 139, 23, 0.267), 0 -4px 3px 0 rgba(241, 139, 23, 0.267);
    }

    .test:hover {
        background-color: #131313; 
    }
    .list-title {
        font-size: 1.4em;
        line-height: 2;
    }
    .list {
        display: flex;
        flex-wrap: wrap;
        justify-content: center;
        padding: 1%;
        font-size: 1.3em;
        margin-bottom: 3%;
    }
    .container {
        display: flex;
        flex-direction: column;
        width: 100%;
    }

    .container img {
        box-shadow: 0px 3px 30px 2px rgba(0, 0, 0, 0.733);
    }

    .container .drinks {
        margin-bottom: 5%;
        background-image: radial-gradient(circle, rgba(219, 154, 57, 0.623), rgba(156, 78, 5, 0.541));
        text-shadow: 2px 2px 1px#000;
    }

    a {
        color: white;
        transition: color 0.3s ease;
        cursor: pointer;
    }
    a:hover {
        color: #cf8205;
        text-decoration: underline;
    }
   
    @media screen and (max-width: 1024px) {
        .category-container {
            padding: 2%;
        }
        .categorys {
            flex-direction: column;
        }
    }
    @media screen and (max-width: 750px) {
        .category-container {
            min-height: 57vh;
        }
        .list {
            margin-bottom: 7%;
            width: 90%;
        }
        .drinks img {
            max-width: 10%;
        }
        .listOfDrinks {
            line-height: 3;
            padding: 5%;
        }
    }

</style>