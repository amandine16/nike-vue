<template>
  <div class="d-flex">
    <div class="filters col-2">
      <h2>Filters</h2>
      <div class="filterGenre">
        <div class="form-check">
          <!-- <checkbox-filter
            v-model="checkGenre"
            v-bind:valeur="Femme"
          ></checkbox-filter>  -->
          <p>Sexe({{ this.checkGenre.length }})</p>
          <input
            v-on:click="check_one('sexe')"
            v-model="checkGenre"
            type="checkbox"
            id="female"
            value="Femme"
            class="form"
          />
          <label for="female">Femme</label>
        </div>
        <div class="form-check">
          <input
            v-on:click="check_one('sexe')"
            v-model="checkGenre"
            type="checkbox"
            id="male"
            value="Homme"
            class="form"
          />
          <label for="male">Homme</label>
        </div>
        <div class="form-check">
          <input
            v-on:click="check_one('sexe')"
            v-model="checkGenre"
            type="checkbox"
            id="mixte"
            value="Mixte"
            class="form"
          />
          <label for="female">Mixte</label>
        </div>
      </div>
      <!-- Sport -->
      <div class="filterPrice">
        <div class="form-check">
          <p>Sport({{ this.checkSport.length }})</p>
          <input
            v-on:click="check_one('sport')"
            v-model="checkSport"
            type="checkbox"
            id="Football"
            value="Football"
            class="form"
          />
          <label for="Football">Football</label>
        </div>
        <div class="form-check">
          <input
            v-on:click="check_one('sport')"
            v-model="checkSport"
            type="checkbox"
            id="Running"
            value="Running"
            class="form"
          />
          <label for="Running">Running</label>
        </div>
        <div class="form-check">
          <input
            v-on:click="check_one('sport')"
            v-model="checkSport"
            type="checkbox"
            id="Basket"
            value="Basket"
            class="form"
          />
          <label for="Basket">Basket</label>
        </div>
        <div class="form-check">
          <ul class="listColors">
            <li
              v-for="(color, index) in colors"
              :style="{
                color: activeColor[index],
              }"
              :key="index"
            >
              {{ color }}
            </li>
          </ul>
        </div>
      </div>
      <!-- Price -->
      <!-- <div class="filterPrice">
        <div class="form-check">
          <p>Recherche par prix({{ this.checkPrice.length }})</p>
          <input
            v-on:click="checkPrice(50)"
            v-model="checkPrice"
            type="checkbox"
            id="moins50"
            value="50"
            class="form"
          />
          <label for="moins50">Moins de 50 €</label>
        </div>
      </div> -->
    </div>

    <div class="results col-10">
      <h2>Results</h2>
      <li v-for="(genre, index) in checkGenre" :key="index">{{ genre }}</li>
      <!-- Affichage des résultats de recherche -->
      <div class="card-deck">
        <div
          v-for="(result, index) in filterGenre"
          v-bind:key="index"
          class="card"
        >
          <OneCard
            :id="index"
            :title="result.article"
            :genre="result.sexe"
            :price="result.price"
            :picture="result.photo"
            :color="result.couleur"
            :sport="result.sport"
          ></OneCard>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import data from "../../assets/data/products.json";
import OneCard from "../Cards/OneCard";
// Essaie de création d'un composant pour les input filter (échec)
// import CheckboxFilter from "../CheckboxFilter";

export default {
  name: "Filters",
  data() {
    return {
      checkGenre: [],
      checkSport: [],
      checkPrice: [],
      resultFilter: [],
      data: data,
      colors: [],
      activeColor: [],
    };
  },
  components: {
    OneCard,
    // CheckboxFilter,
  },
  computed: {
    //   filtre par sexe ou sport
    filterGenre: function() {
      return this.data
        .filter((article) => article.sexe.match(this.checkGenre))
        .filter((article) => article.sport.match(this.checkSport));
    },
  },
  methods: {
    //   Une seule selection possible pour le filtre
    check_one: function(genre) {
      if (genre === "sexe") {
        this.checkGenre = [];
      } else {
        this.checkSport = [];
      }
    },
    // checkPrice: function(price){

    // }
  },
  mounted() {
    // Création d'un tableau qui contient toutes les couleurs proposées, sans doublons ni chaine de charactères vides
    let tab = "";
    let newTab = [];
    for (let i = 0; i < data.length; i++) {
      tab = data[i].couleur.split(", ");
      for (let y = 0; y < tab.length; y++) {
        if (newTab.indexOf(tab[y].toLowerCase()) === -1 && tab[y] !== "") {
          newTab.push(tab[y].toLowerCase());
        }
      }
    }
    this.colors = newTab;
    this.activeColor = newTab;
    //  Création d'un tableau qui converti les couleurs fécrites en français, en anglais (qui servira ensuite pour afficher dynamiquement le filtre des couleurs)
    let newTabActiveColor = [];
    for (let w = 0; w < this.activeColor.length; w++) {
      if (this.activeColor[w] === "noir") {
        newTabActiveColor.push("black");
      }
      if (this.activeColor[w] === "rouge") {
        newTabActiveColor.push("red");
      }
      if (this.activeColor[w] === "vert") {
        newTabActiveColor.push("green");
      }
      if (this.activeColor[w] === "blanc") {
        newTabActiveColor.push("white");
      }
      if (this.activeColor[w] === "jaune") {
        newTabActiveColor.push("yellow");
      }
      if (this.activeColor[w] === "bleu") {
        newTabActiveColor.push("blue");
      }
      if (this.activeColor[w] === "rose") {
        newTabActiveColor.push("pink");
      }
      if (this.activeColor[w] === "gris") {
        newTabActiveColor.push("grey");
      }
    }
    this.activeColor = newTabActiveColor;
    console.log(this.activeColor);
  },
};
</script>
<style scoped src="../Cards/card-css.css"></style>
