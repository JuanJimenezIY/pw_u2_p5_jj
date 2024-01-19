<template>
  <div class="container">
    <img :src="urlImg" alt="No se puede">
    <label for="">{{texto}}</label>
  </div>
</template>

<script>
export default {
    props:{
        texto:{
            type:String
        },
        urlImg:{
            type:String
        }
    }

}
</script>

<style>
img{
    width: 200px;
    height: 300px;
}
</style>