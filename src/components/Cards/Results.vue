<template>
  <div class="card-deck">
    <div v-for="(result, index) in data" v-bind:key="index" class="card">
      <OneCard
        :id="index"
        :title="result.article"
        :genre="result.sexe"
        :price="result.price"
        :picture="result.photo"
        :color="result.couleur"
      ></OneCard>
    </div>
  </div>
</template>

<script>
import OneCard from "../Cards/OneCard";

export default {
  name: "Results",
  props: ["data"],

  components: {
    OneCard,
  },
};
</script>

<style scoped src="./card-css.css"></style>
