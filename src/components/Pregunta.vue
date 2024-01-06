<template>
  <img
    src="https://yesno.wtf/assets/no/14-cb78bf7104f848794808d61b9cd83eba.gif"
    alt="np se puede visualizar "
  />

<div class="dark"></div>
  <div class="container">
    <input v-model="pregunta" type="text" />
    <p>Recuerda que debes terminar con el signo de interrogación</p>
    <h2>{{pregunta}}</h2>
    <h1>SI,NO...</h1>
  </div>
</template>

<script>
export default {

  data(){
    return{
      pregunta:"Voy a ser millonario?"
    };
  },
  watch:{
    pregunta(value, oldvalue){
      console.log(value)
         console.log(oldvalue)
         if(!value.includes('?')) return;
         
         //consumo del api
         this.consumirAPI()
    },
  },
  methods:{
     async consumirAPI(){

        const {answer,image}=await fetch('https://yesno.wtf/api').then(respuesta=>respuesta.json())
        console.log(answer)
         console.log(image)
    }
  }
};
</script>

<style scoped>
.dark, img{
    height: 100vh;
    width: 100vw;
    max-height: 100%;
    max-width: 100%;
    position: fixed;
    top: 0px;
    left: 0px;
   

}
.dark{
 background: rgba(0, 0, 0, 0.4);

}
input{
    width: 250px;
    padding: 10px 15px;
    border-radius: 5px;
    border: none;
    margin-bottom: 10px;
}
.container{
  position: relative;
}
input:focus{
  outline: none;
}
p{
  color: white;
  font-size: 20px;
  margin-top: 10px;
}
h1,h2{
  color: white;
}
h2{
  margin-top: 150px;
}
</style>