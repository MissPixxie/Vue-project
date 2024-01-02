<template>
  <div class="mainDrinkView">
    <GetRandomDrinkApi />
  </div>
</template>

<script>
import GetRandomDrinkApi from "@/components/GetRandomDrinkApi.vue";

export default {
  name: "DrinkView",
  components: { GetRandomDrinkApi },
  data() {
    return {
      activeComponent: "GetRandomDrinkApi",
    };
  },
};
</script>
