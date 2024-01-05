<template>
  <h2>{{ titulo }}</h2>
  <p>{{ counter }} <sup>2</sup> = {{ obtenerCuadradoComputado }}</p>
  <button @click="incrementar()">+1</button>
  <button @click="decrementar()">-1</button>
</template>

<script>
export default {
  /*props: ["titulo","valor"],*/
  props: {
    titulo: String,
    valor: {
      type: Number,
      required: true,
      default: 100,
      validator(value) {
        if (value > 0) {
          console.log("error");
        }
        return value > 0;
      },
    },
  },
  data() {
    return {
      counter: this.valor,
    };
  },

  methods: {
    obtenerCuadrado() {
      console.log("se calcula el cuadrado");
      return this.counter * this.counter;
    },
    incrementar() {
      return this.counter++;
    },
    decrementar() {
      return this.counter--;
    },
  },
  computed: {
    obtenerCuadradoComputado() {
      console.log("se calcula el cuadrado computado");
      return this.counter * this.counter;
    },
  },
};
</script>

<style>
button {
  background: rgb(113, 196, 113);
  border-radius: 5px;
  border: 3px solid rgb(255, 255, 255);
  color: white;
  cursor: pointer;
  margin: 0px 5px;
  padding: 5px 15px;
  font-family: Arial, Helvetica, sans-serif;
  font-weight: 600;
}
button:hover {
  background: #5aa67b;
}
h2{
  font-family: Helvetica;
  color: #5aa67b;
}
p{
  color: rgb(21, 75, 65);
  font-size: 20px;
}
*{background: #d3ffd4;}
</style>