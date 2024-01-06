<template>
  <body>
    <header></header>
    <nav></nav>
    <section>
      <div class="container">
        <div class="calculadora">
          <div id="idResultado" class="display">{{ resultado }}</div>
      
          <button class="span-2" @click="reset()">C</button>
          <button @click="back()">&larr;</button>
          <button @click="operacion('/')">/</button>
          <button @click="numeros(7)">7</button>
          <button @click="numeros(8)">8</button>
          <button @click="numeros(9)">9</button>
          <button @click="operacion('*')">&#215;</button>
          <button @click="numeros(4)">4</button>
          <button @click="numeros(5)">5</button>
          <button @click="numeros(6)">6</button>
          <button @click="operacion('-')">&#8722;</button>
          <button @click="numeros(1)">1</button>
          <button @click="numeros(2)">2</button>
          <button @click="numeros(3)">3</button>
          <button @click="operacion('+')">&#43;</button>
          <button @click="numeros(0)" class="span-2">0</button>
          <button @click="numeros('.')">&#46;</button>
          <button @click="calcular()">&#61;</button>
        </div>
      </div>
    </section>
    <footer></footer>
  </body>
</template>

<script>
export default {
 
  data() {
    return {
      resultado: "",
      num1: "",
    };
  },
  methods: {
    reset() {
      this.resultado = "";
    },
    operacion(op) {
      this.num1 = this.resultado + op;
      this.resultado = "";
    },
    numeros(num) {
      this.resultado += num;
    },
    back() {
      this.resultado = this.resultado.slice(0, -1);
    },
    calcular() {
      let res = eval(this.num1 + this.resultado);
      this.resultado = res.toString();
    },
  },
};
</script>

<style>
.container {
  display: flex;
  align-items: center;
  justify-content: center;
}
.calculadora {
  display: grid;
  /* grid-template-columns: 75px 75px 75px 75px;*/
  /*grid-template-columns: 20px repeat(4,75px);*/
  grid-template-columns: repeat(4, 75px);

  grid-template-rows: 150px repeat(5, 75px);
  background-color: #00916e;
  padding: 15px;
  border-radius: 32px;
  box-shadow: 15px 10px 5px 5px #00000033;
}
.display {
  margin: 10px 10px 20px 10px;
  grid-column: span 4;
  padding: 25px 15px;
  background-color: #363636;
  border-radius: 32px;
  text-align: right;
  font-size: 20px;
  font-family: sans-serif;
  box-shadow: 0px 0px 0px 10px #00000033;
}
button {
  cursor: pointer;
  margin: 5px;
  padding: 0px;
  border-radius: 32px;
  border: none;
  background-color: #017a5e;
  box-shadow: 5px 5px 10px 2px #00000040;
  font-size: 22px;
}
button:hover {
  background-color: #575b5f;
}
button:active {
  background-color: #42b095;
}
.span-2 {
  grid-column: span 2;
}
body {
  background-color: #343f4c;
}

* {
  color: white;
  font-family: "Trebuchet MS", "Lucida Sans Unicode", "Lucida Grande",
    "Lucida Sans", Arial, sans-serif;
}
</style>