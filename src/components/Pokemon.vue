<template>
  <div id="app">
    <div class="card">
      <div class="card-image">
        <figure>
          <img :src="pokemon.front" height="120px" width="120px" />
        </figure>
      </div>
      <div class="card-content">
        <div class="media">
          <div class="media-left">
            <div class="number">
              {{ numero }}
            </div>
          </div>
          <div class="media-content">
            <p class="title is-4">{{ name | uppercase }}</p>
            <p class="subtitle is-6">{{ pokemon.type | tipo }}</p>
          </div>
        </div>

        <div class="content"></div>
      </div>
    </div>

    <hr />
  </div>
</template>

<script>
import axios from "axios";

export default {
  created: function () {
    axios.get(this.url).then((dados) => {
      this.pokemon.type = dados.data.types[0].type.name;
      this.pokemon.front = dados.data.sprites.front_default;
    });
  },
  data() {
    return {
      pokemon: {
        type: "",
        front: "",
      },
    };
  },
  props: {
    numero: Number,
    name: String,
    url: String,
  },
  filters: {
    uppercase: function (value) {
      var novo = value[0].toUpperCase() + value.slice(1);
      return novo;
    },
    tipo: function (value) {
      var novotipo = value[0].toUpperCase() + value.slice(1);
      return novotipo;
    },
  },
};
</script>

<style scoped>
.number {
  padding: 2px;
  background-color: rgb(3, 96, 119);
  color: white;
  border-radius: 50%;
  height: 30px;
  width: 30px;
  font-weight: bolder;
  font-size: 13px;
  font-family: "Franklin Gothic Medium", "Arial Narrow", Arial, sans-serif;
}

figure {
  text-align: center;
}

#app {
  background-color: azure;
}
</style>