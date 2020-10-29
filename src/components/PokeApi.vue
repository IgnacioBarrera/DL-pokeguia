<template>
  <div class="text-center">
    <img src="https://raw.githubusercontent.com/PokeAPI/media/master/logo/pokeapi_256.png" alt="pokeAPI" class="pb-3">
    <form @submit.prevent="RegistrarPoke">
      <label class="mr-2">Nombre:</label>
      <input type="text" v-model="nombre_pokemon">
      <button type="submit" class="btn btn-success ml-2">Buscar</button>
    </form>
    <img :src="imagenPoke" :alt="this.namePoke">
    <h2>Nombre pokemón: {{namePoke}}</h2>
    <div>
      <h3>Habilidades:</h3>
      <ul v-for="(habilidad, index) in habiPoke" :key="index">
      <li>
        {{habilidad.ability.name}}
      </li>
      </ul>
    </div>
    <div>
      <h3>Movimientos:</h3>
      <ul v-for="(movimiento, index) in movPoke" :key="index">
      <li>
        {{movimiento.move.name}}
      </li>
      </ul>
    </div>
    
  </div>
</template>

<script>
import axios from 'axios';
export default {
  name: 'PokeApi',
  data() {
    return {
      nombre_pokemon: '',
      namePoke: '',
      habiPoke: '',
      movPoke: '',
      imgPoke: '',
    }
  },
  methods: {
    RegistrarPoke(){
      axios.get(`https://pokeapi.co/api/v2/pokemon/${this.nombre_pokemon}`)
      .then((resultado) => {
      this.namePoke = resultado.data.name;
      this.habiPoke = resultado.data.abilities;
      this.movPoke = resultado.data.moves;
      this.imgPoke = resultado.data.sprites;
    })
    .catch(error=>console.error(error));
    this.nombre_pokemon = "";
    }
  },
  computed: {
    imagenPoke(){
      return this.imgPoke.front_default;
    }
  },
  created() {
    axios.get(`https://pokeapi.co/api/v2/pokemon/pikachu`)
    .then((resultado) => {
      this.namePoke = resultado.data.name;
      this.habiPoke = resultado.data.abilities;
      this.movPoke = resultado.data.moves;
      this.imgPoke = resultado.data.sprites;
    })
    .catch(error=>console.error(error));
  },
}

</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
ul {
      list-style-type: none;
}
button {
  border-radius: 20px;
}
</style>
