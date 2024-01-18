<template>
  <h1>Adivina el Pokemon</h1>
    <PokemonImagen :pokemonId="6" :showPokemon="true"/>
    <PokemonOpciones />
</template>

<script>

import PokemonImagen from '../components/PokemonImagen.vue'
import PokemonOpciones from '../components/PokemonOpciones.vue'

import obtenerPokemonsIdFachada from '../helpers/pokemonHelper'


obtenerPokemonsIdFachada()

export default {
components:{
    PokemonImagen,
     PokemonOpciones
},
mounted(){
  console.log('Se monto el componente PokemonPage')
  this.cargaInicial()
  },
methods:{
  async cargaInicial(){
  const arregloPokemons= await obtenerPokemonsIdFachada();
  console.log('desde componente');
  console.log(arregloPokemons);
},
  
}
}
</script>

<style>

</style>