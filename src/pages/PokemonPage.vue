<template>
<h1 v-if="!pokemonGanador">Espere por favor mientras carga...</h1>
  <div  v-else >
    <h1>Adivina el Pokemon</h1>
    <PokemonImagen :pokemonId="pokemonGanador.id" :showPokemon="mostrarPokemon" />
    <PokemonOpciones @selecciono="revisarClick($event)" :pokemons="pokemonsArr" />
  </div>
</template>

<script>
import PokemonImagen from "../components/PokemonImagen.vue";
import PokemonOpciones from "../components/PokemonOpciones.vue";

import obtenerPokemonsIdFachada from "../helpers/pokemonHelper";

obtenerPokemonsIdFachada();

export default {
  components: {
    PokemonImagen,
    PokemonOpciones,
  },

  beforeCreate() {
    console.log("antes de crear el cmponente");
  },
  created() {

    console.log("se creo el componente");
  },
  beforeMount() {
    console.log("antes de qe se monte el componente en la pagina");
  },
  mounted() {
    console.log("Se monto el componente PokemonPage");
    this.cargaInicial();
  },
  beforeUpdate() {
    console.log("Antes de que se actualice el componente");
  },
  updated() {
    console.log("Se actualiza el componente");
  },
  beforeDestroy() {
    console.log("Antes de que se destruya");
  },
  destroyed() {
    console.log("Destruido");
  },
   
  methods: {
    async cargaInicial() {
      const arregloPokemons = await obtenerPokemonsIdFachada();
      console.log("desde componente");
      console.log(arregloPokemons);
      this.pokemonsArr = arregloPokemons;
      const indiceGanador = Math.floor(Math.random() * 4);
    
      this.pokemonGanador = this.pokemonsArr[indiceGanador];
  
    },
    revisarClick(datoRecibido){
      console.log('dio click y reporto desde el padre')
      console.log(datoRecibido.hobby)
      this.mostrarPokemon=true
    }
  
  },
   data() {
      return {
        pokemonsArr: [],
        pokemonGanador:null,
        mostrarPokemon:false
      };
    },
};
</script>

<style>
</style>