<template>
  <div id="app">
    <div class="d-flex flex-wrap container">
      <div><Filters></Filters></div>
      <!-- <div class="col-10"><Results v-bind:data="data"></Results></div> -->
    </div>
  </div>
</template>

<script>
// import Results from "./components/Cards/Results";
import Filters from "./components/Filters/Filters";
// import data from "./assets/data/products.json";

export default {
  name: "App",
  data() {
    return {
      // data,
    };
  },
  components: {
    // Results,
    Filters,
  },
};
</script>

<style></style>
