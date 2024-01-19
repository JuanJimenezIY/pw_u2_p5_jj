<template>
  <!--<PokemonPage/>-->
  <div class="container" v-if="mostrarJuego">
  <h1>Casino Pokemon</h1>
  <h2>Puntaje:{{ puntaje }}</h2>
  <h2>Intentos:{{ intento }}</h2>
  <Imagen :texto="texto1" :urlImg="url1" />
  <Imagen :texto="texto2" :urlImg="url2" />
  <Imagen :texto="texto3" :urlImg="url3" />
  <button v-on:click="jugar">Jugar</button>
  </div>

  <div v-if="mostrarPerdedor">
<h1>Haz utilizado tus 5 intentos</h1>
<h1>El juego ha terminado, intentalo nuevamente</h1>
<button @click="reiniciar">Reiniciar</button>
  </div>
  <div v-if="mostrarGanador">
<h1>Puntaje: {{puntaje}}</h1>
<h1>Felicitaciones has ganado un premio de $10,000,00</h1>
<button @click="reiniciar">Reiniciar</button>
  </div>

</template>

<script>
//import PokemonPage from './pages/PokemonPage.vue'
import Imagen from "./components/Imagen.vue";

export default {
  name: "App",
  components: {
    // PokemonPage
    Imagen,
  },
  data() {
    return {
      puntaje: 0,
      intento: 0,
      url1: "https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/other/dream-world/1.svg",
      url2: "https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/other/dream-world/2.svg",
      url3: "https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/other/dream-world/3.svg",
      texto1: "XXXXXXXX",
      texto2: "XXXXXXXX",
      texto3: "XXXXXXXX",
      mostrarGanador: false,
      mostrarPerdedor: false,
      mostrarJuego:true
    };
  },
  methods: {
    async jugar() {
      this.texto1 = "charmander";
      //instancia 1
      const data1 = await this.consumirAPI();
      this.texto1 = data1.answer;
      this.url1 = data1.image;
      //instancia 2
      const data2 = await this.consumirAPI();
      this.texto2 = data2.answer;
      this.url2 = data2.image;
      //instancia 3
      const data3 = await this.consumirAPI();
      this.texto3 = data3.answer;
      this.url3 = data3.image;
      this.evaluarResultado();
    },
    async consumirAPI() {
      return await fetch("https://yesno.wtf/api").then((r) => r.json());
    },
    evaluarResultado() {
      this.intento++;
      if (
        this.texto1 === "yes" &&
        this.texto2 === "yes" &&
        this.texto3 === "yes"
      ) {
        this.puntaje += 5;
      } else if (
        (this.texto1 === "yes" && this.texto2 === "yes") ||
        (this.texto2 === "yes" && this.texto3 === "yes") ||
        (this.texto1 === "yes" && this.texto3 === "yes")
      ) {
        this.puntaje += 2;
      } else if (
        this.texto1 === "yes" ||
        this.texto2 === "yes" ||
        this.texto3 === "yes"
      ) {
        this.puntaje += 1;
      }

      if (this.puntaje >= 10) {
        this.mostrarGanador=true;
           this.mostrarPerdedor=false;
        this.mostrarJuego=false;
      }
      if(this.intento===5){
        this.mostrarPerdedor=true;
        this.mostrarGanador=false;
        this.mostrarJuego=false;
      }

    },
    reiniciar(){

      this.puntaje=0;
      this.intento= 0;
      this.url1= "https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/other/dream-world/1.svg";
      this.url2= "https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/other/dream-world/2.svg";
      this.url3= "https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/other/dream-world/3.svg";
      this.texto1= "XXXXXXXX";
      this.texto2= "XXXXXXXX";
      this.texto3= "XXXXXXXX";
      this.mostrarGanador= false;
      this.mostrarPerdedor= false;
      this.mostrarJuego=true;
    }
  },
};
</script>

<style>

  .container{
    display: grid;
    justify-content: center;
    align-content: center;
     grid-template-columns: repeat(4,200px);
  }

h1{
  grid-column: span 4;
}
h2{
  grid-column: span 2;
}
img{
  grid-column: span 1;;
}
</style>
