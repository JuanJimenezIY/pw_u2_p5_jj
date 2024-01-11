<template>
  <div class="container">
    <h1>Busqueda pokemon</h1>
    <p class="form" type="Id:">
      <input @keypress.enter="consumirAPI()" type="text" v-model="id" />
    </p>
    <p>Presione Enter para disparar la busqueda</p>
    <div class="form">
      <p type="Name:">
        <input type="text" v-model="nombre" />
      </p>
      <p type="Weight:">
        <input type="text" v-model="weight" />
      </p>
      <p type="Experiencia Base:">
        <input type="text" v-model="experience" />
      </p>
    </div>
  </div>
</template>
    
<script>
export default {
  data() {
    return {
      id: null,
      nombre: null,
      weight: null,
      experience: null,
    };
  },
  watch: {},
  methods: {
    async consumirAPI() {
      this.nombre = "Pensando....";
      this.weight = "Pensando....";
      this.experience = "Pensando....";
      const { name, weight, base_experience } = await fetch(
        "https://pokeapi.co/api/v2/pokemon/" + this.id
      ).then((respuesta) => respuesta.json());

      this.nombre = name;
      this.experience = base_experience;
      this.weight = weight;
    },
  },
};
</script>

<style>
.container {
  display: grid;
  justify-content: center;
  align-items: center;
}

.form {
  background-color: #9db1a7;
  border-radius: 8px;
  padding: 20px 30px;
}
p{
    color: rgb(31, 114, 81);
}
p::before {
  content: attr(type);
  display: flex;
}
input {
  width: 400px;
  background: rgb(240, 240, 240);

  color: rgb(53, 14, 14);
}
h1{
    color: rgb(176, 45, 45);
}
body{
    font-family: Arial, Helvetica, sans-serif
}
</style>