<template>
  <div v-show="!mobile">
    <nav class="navbar">
      <span><router-link to="/">Home</router-link> </span>
      <span> | </span>
      <span><router-link to="/about">About</router-link></span>
      <span> | </span>
      <span><router-link to="/drinks">Drinks</router-link></span>
      <span> | </span>
      
      <div class="menu-item" @click="isOpen = !isOpen">

      <a href ='#'>Kategori</a>
      <svg viewBox="0 0 1030 638" width="10">
            <path d="M1017 68L541 626q-11 12-26 12t-26-12L13 68Q-3 49 6 24.5T39 0h952q24 0 33 24.5t-7 43.5z" fill="#FFF"></path>
        </svg>
        <transition name="fade" appear>
        <div class="sub-menu" v-if="isOpen">
              <ul>
                <li v-for="(drink, index) in newCategorys" :key="index">
                    <router-link :to="{path: '/category/' + drink}">{{ drink }}</router-link>                   
                </li>
              </ul>
        </div>
        </transition>
      </div>
    </nav>
  </div>
  <div v-show="mobile">
    <nav class="navbar">
      <div class="icon">
        <i @click="isMobileOpen = !isMobileOpen" v-show="mobile" class="fa fa-bars" :class="{'icon-active' : mobileNav}"></i>

      </div>
      <transition name="mobile-nav" appear>
        <div v-if="isMobileOpen" class="dropdown-nav">
          <span><router-link to="/">Home</router-link></span>
          <span><router-link to="/about">About</router-link></span>
          <span><router-link to="/api">Drinks</router-link></span>
          <div class="menu-item" @click="isOpen = !isOpen">
            <a href ='#'>Kategori</a>
            <svg viewBox="0 0 1030 638" width="10">
                  <path d="M1017 68L541 626q-11 12-26 12t-26-12L13 68Q-3 49 6 24.5T39 0h952q24 0 33 24.5t-7 43.5z" fill="#FFF"></path>
              </svg>
              <transition name="fade" apear>
              <div class="sub-menu" v-if="isOpen">
                    <ul>
                      <li v-for="(drink, index) in newCategorys" :key="index" @click="isMobileOpen = !isMobileOpen">
                          <router-link :to="{path: '/category/' + drink}">{{ drink }}</router-link>                   
                      </li>
                    </ul>
              </div>
              </transition>
            </div>
        </div>
      </transition>
    </nav>
  </div>
</template>

<script>
//import { vClickOutside } from '@vueuse/components'
export default {
    name: 'headerComponent',
    data() {
      return {
          isOpen: false,
          isMobileOpen: false,
          posts: [],
          newCategorys: [],
          mobile: null,
          mobileNav: null,
          windowWidth: null,
      }
    },
    beforeCreate(){
      const newCategorys = [];
      fetch('https://www.thecocktaildb.com/api/json/v1/1/list.php?c=list')
          .then((response) => response.json())
          .then((json) => {
              this.posts = json
              const filterCharacters = json.drinks
              //Eftersom det är nestlat så används 2 loopar, första loopen ger objekt med key: strCategory, value: kategorin
              for (const property in filterCharacters) {
                // Andra loopen tar alla value och lägger dom i variabeln kategori
                for ( const value in filterCharacters[property]) {
                  let kategori = filterCharacters[property][value];
                  // Om value inte innehåller " / " så pushas dessa in i arrayen newCategorys
                  if ( !kategori.includes(" / ")) {
                    newCategorys.push(kategori);
                    //console.log(newCategorys)
                  }
                  else {
                    // Om value innehåller " / " ersätts detta först med and och pushas sedan in i arrayen newCategorys
                    let ny = kategori.replace(" / ", " and ");
                    newCategorys.push(ny);
                  } 
                }
          }
          this.newCategorys = newCategorys;
          console.log(newCategorys)
          })
    },
    created(){
      window.addEventListener('resize', this.checkScreen);
      this.checkScreen();
  },
  methods: {
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
    },
  }
}
</script>

<style scoped>

.navbar {
display: flex;
justify-content: space-evenly;
background-color: rgb(12, 12, 12);
padding: 2%;
box-shadow: 0px 3px 20px 2px rgba(0, 0, 0, 0.589);
font-family: 'Taviraj', serif;
font-size: 1.3em;
text-transform: uppercase;
}

nav a, span {
font-weight: bold;
color: rgb(224, 224, 224);
text-decoration: none;
transition: color 0.3s ease;
}

a:hover {
text-decoration: underline;
color: rgb(250, 150, 35);
}

nav a.router-link-exact-active {
color: #cf8205;
}

.sub-menu {
font-size: 0.8em;
}

.icon {
color: white;
font-size: 1.3em;
text-align: right;
padding: 1%;
}

i {
cursor: pointer;
font-size: 1.2em;
}

.js-is-hidden {
display: none;
}
@media only screen and (max-width: 750px) {
.navbar {
  flex-direction: column;
}
.navbar span {
  display: block;
  line-height: 1.5;
}
.sub-menu {
font-size: 0.9em;
}
}
</style>