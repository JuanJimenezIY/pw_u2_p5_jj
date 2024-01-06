<template>
  <img alt="Vue logo" src="./assets/logo.png">
  <Calculadora />
    
</template>

<script>
import Calculadora from './components/Calculadora.vue';


export default {
  name: 'App',
  components: {
      
      Calculadora
  },
  methods:{
    calcularValor(){
      return 5+5*100;
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
