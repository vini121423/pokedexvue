<template>
  <div id="#app">
    <div class="img">
      <img src="./assets/pokemon.png" width="30%" height="30%" />
    </div>
    <div class="column is-half is-offset-one-quarter">
      <input
        class="input is-rounded is-primary"
        type="text"
        placeholder="Primeira letra minuscula"
        v-model="busca"
      />
      <div class="button-div">
        <button class="button is-primary" @click="buscarPokemons">
          Buscar
        </button>
      </div>
      <div v-for="(pokemon, index) in arrayFilter" :key="pokemon.url">
        <Pokemon :name="pokemon.name" :url="pokemon.url" :numero="index + 1" />
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
import Pokemon from "./components/Pokemon";

export default {
  name: "App",
  data() {
    return {
      pokemons: [],
      arrayFilter: [],
      busca: "",
    };
  },
  created: function () {
    axios
      .get("https://pokeapi.co/api/v2/pokemon?limit=30&offset=0")
      .then((dados) => {
        this.pokemons = dados.data.results;
        this.arrayFilter = dados.data.results;
      });
  },
  components: {
    Pokemon,
  },
  methods: {
    buscarPokemons: function () {
      this.arrayFilter = this.pokemons;

      if (this.busca == "" || this.busca == " ") {
        return (this.arrayFilter = this.pokemons);
      } else {
        return (this.arrayFilter = this.pokemons.filter(
          (pokemon) => pokemon.name == this.busca
        ));
      }
    },
  },
  computed: {
    exibirResultados: function () {
      if (this.busca == "" || this.busca == " ") {
        return this.pokemons;
      } else {
        return this.pokemons.filter((pokemon) => pokemon.name == this.busca);
      }
    },
  },
};
</script>

<style>
.img {
  text-align: center;
  padding:5px;
}
.button-div {
  align-items: center;
  text-align: center;
  padding: 10px;
}

button{
  width: 200px;
  height: 70px;
  font-weight: bolder;
  font-size: 15px;
}
</style>
