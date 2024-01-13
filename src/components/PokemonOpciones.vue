<template>
  <div class="options-container">
        <ul>
            <li>1</li>
            <li>2</li>
            <li>3</li>
            <li>4</li>
        </ul>


  </div>
</template>

<script>
export default {

}
</script>

<style>
.options-container{
 
    display: flex;
    justify-content: center;
}
ul{
    list-style-type: none;
}
li{
    background:rgb(255, 255, 255);
    border-radius: 5px;
    border: 1px solid rgba(51, 13, 13, 0.2);
    width: 250px;
    margin-bottom: 10px;
    cursor: pointer;
}
li:hover{
    background: rgba(0, 0, 0, 0.1);
}
</style>