<template>
  <div class="form-check">
    <p>Sexe !!!</p>
    <input
      :value="checkGenre"
      @input="$emit('update:checkGenre', $event.target.value)"
      type="checkbox"
      id="valeur"
      class="form"
    />
    <label for="female">Femme</label>
  </div>
</template>

<script>
export default {
  name: "CheckboxFilter",
  props: ["checkGenre", "valeur"],
};
</script>
