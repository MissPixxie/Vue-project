<template>
  <div class="mainCategoryView">
    <GetCategoryApi />
  </div>
</template>

<script>
import GetCategoryApi from "@/components/GetCategoryApi.vue";

export default {
  name: "CategoryView",
  components: { GetCategoryApi },
};
</script>
