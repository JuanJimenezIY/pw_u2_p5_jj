<template>
  <div class="pokemons-container">
      <img
      :src="imagenFuente"
      alt="No se puede visualizar"
    
      class="ocultar"
    />
    <img :src="imagenFuente" alt="No se puede visualizar" v-if="showPokemon" />
  
  </div>
</template>

<script>
export default {
  props: {
    pokemonId: {
      type: Number,
      required: true,
    },
    showPokemon: {
      type: Boolean,
      required: true,
      default: false,
    },
  },
  computed: {
    imagenFuente() {
      return `https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/other/dream-world/${this.pokemonId}.svg`;
    },
  },
};
</script>

<style>
.ocultar {
  filter: brightness(0);
}
img {
  height: 200px;
  position: absolute;
  right: 43%;
}
.pokemons-container {
  height: 200px;
}
</style>