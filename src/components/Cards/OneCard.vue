<template>
  <div>
    <img
      class="card-img-top"
      :src="require(`../../assets/img/${picture}`)"
      :alt="title"
    />
    <div class="card-body">
      <h5 class="card-title">{{ title }}</h5>
      <p class="card-text">Chaussure pour {{ genre }}</p>
      <p class="card-text">{{ sport }}</p>
      <p class="card-text">
        <small class="text-muted">Couleur {{ color }}</small>
      </p>
    </div>
  </div>
</template>

<script>
export default {
  name: "OneCard",
  props: ["id", "title", "genre", "price", "picture", "color", "sport"],
};
</script>

<style src="./card-css.css"></style>
