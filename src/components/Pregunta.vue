<template>
  <img v-if="img !== null" v-bind:src="img" alt="No se puede visualizar " />

  <div class="dark"></div>
  <div class="container">
    <input v-model="pregunta" type="text" />
    <p>Recuerda que debes terminar con el signo de interrogación(?)</p>
    <div v-if="preguntaValida">
      <h2>{{ pregunta }}</h2>
      <h1>{{ respuesta }}</h1>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      pregunta: null,
      respuesta: null,
      img: null,
      preguntaValida: false,
    };
  },
  watch: {
    pregunta(value, oldvalue) {
      this.preguntaValida=false;
      console.log(value);
      console.log(oldvalue);
      if (!value.includes("?")) return;

      //consumo del api
      this.consumirAPI();
      this.preguntaValida=true
    },
  },
  methods: {
    async consumirAPI() {
      this.respuesta='Pensando.' 
      this.respuesta='Pensando..' 
      this.respuesta='Pensando...' 
      this.respuesta='Pensando....' 
      const { answer, image } = await fetch("https://yesno.wtf/api").then(
        (respuesta) => respuesta.json()
      );
      console.log(answer);
      console.log(image);
      this.respuesta = answer==='yes'? 'SI!': 'NO!';
      this.img = image;
    }

  },
};
</script>

<style scoped>
.dark,
img {
  height: 100vh;
  width: 100vw;
  max-height: 100%;
  max-width: 100%;
  position: fixed;
  top: 0px;
  left: 0px;
}
.dark {
  background: rgba(0, 0, 0, 0.4);
}
input {
  width: 250px;
  padding: 10px 15px;
  border-radius: 5px;
  border: none;
  margin-bottom: 10px;
}
.container {
  position: relative;
}
input:focus {
  outline: none;
}
p {
  color: white;
  font-size: 20px;
  margin-top: 10px;
}
h1,
h2 {
  color: white;
}
h2 {
  margin-top: 150px;
}
</style>