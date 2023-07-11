<template>
    <div class="main">
      <GetRandomDrinkApi />
    </div>    
</template>

<script>

import GetRandomDrinkApi from '@/components/GetRandomDrinkApi.vue';

export default {
    name: 'DrinkView',
    components: { GetRandomDrinkApi },
    data() {
      return {
        activeComponent: 'GetRandomDrinkApi'
      }
    }
}
</script>