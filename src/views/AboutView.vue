<template>
  <div class="about">
      <heroComponent />
      <div class="cards">
        <cardsKomponent title="CARD 1" text="Lorem ipsum dolor sit amet, consectetur adipiscing elit. Pellentesque volutpat orci ac mi maximus, id malesuada ante interdum."/>
        <cardsKomponent title="CARD 2" text="Lorem ipsum dolor sit amet, consectetur adipiscing elit. Pellentesque volutpat orci ac mi maximus, id malesuada ante interdum."/>
        <cardsKomponent title="CARD 3" text="Lorem ipsum dolor sit amet, consectetur adipiscing elit. Pellentesque volutpat orci ac mi maximus, id malesuada ante interdum."/>         
      </div>
    
  </div>
</template>

<script>

import cardsKomponent from '@/components/cards.vue';
import heroComponent from '@/components/hero.vue';

  export default {
    components: { 
      cardsKomponent,
      heroComponent }
}
</script>

<style>

.about {
  font-family: 'Taviraj', serif;
}

  .cards {
    display: flex;
    justify-content: space-around;
  }
  @media only screen and (max-width: 750px) {
        .cards {
            flex-direction: column;
            align-items: center;
        }
    }
</style>