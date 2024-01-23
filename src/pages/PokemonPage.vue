<template>
<h1 v-if="!pokemonGanador">Espere por favor mientras carga...</h1>
  <div  v-else >
    <h1>Adivina el Pokemon</h1>
    <PokemonImagen  :pokemonId="pokemonGanador.id" :showPokemon="mostrarPokemon" />
    <PokemonOpciones v-if="pantalla" @selecciono="revisarClick($event)" :pokemons="pokemonsArr" />
  </div >
  <div v-if="pantallaGanador" class="ganador">

    <h2>Felicidades, has ganado el juego!!</h2>
    <button @click="reiniciar()">Reiniciar juego</button>
  </div>
  <div v-if="pantallaPerdedor" class="perdedor">

    <h2>Has fallado, intentalo de nuevo</h2>
    <button @click="reiniciar()">Reiniciar juego</button>
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
      

      if (this.pokemonGanador.id=== datoRecibido.id) {
        this.mostrarPokemon=true
        this.pantalla=false
        this.pantallaGanador=true
        
      }else{
        this.pantalla=false
        this.pantallaPerdedor=true
      }

    },
    reiniciar(){
     
      this.pokemonsArr = [];
    this.pokemonGanador = null;
    this.mostrarPokemon = false;
    this.pantallaGanador = false;
    this.pantallaPerdedor = false;
    this.pantalla = true;
    this.cargaInicial();
        
    }
  
  },
   data() {
      return {
        pokemonsArr: [],
        pokemonGanador:null,
        mostrarPokemon:false,
        pantallaGanador:false,
        pantallaPerdedor:false,
        pantalla:true
      };
    },
};
</script>

<style>

h1{
  font-size: 40px;
  font-family: Cambria, Cochin, Georgia, Times, 'Times New Roman', serif;
  color: rgb(42, 42, 100);
}
.perdedor{
  color: brown;
}
button{

    background:rgb(250, 255, 255);
    border-radius: 5px;
    border: 3px solid rgba(51, 13, 13, 0.2);
    width: 150px;
    padding: 5px;
    cursor: pointer;
}
button:hover{
    background: rgba(0, 0, 0, 0.1);
}
</style>