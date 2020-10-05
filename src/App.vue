<template>
  <div class="application">
    <div id="logo">
      <img alt="Vue logo" src="./assets/logo.png">
    </div>
    <div>
      <OfferDryTag/> 
    </div>
  </div>
</template>

<script>
import OfferDryTag from "./views/OfferDryTag";

export default {
  name: "App",
  components: { OfferDryTag }
}
</script>

<style>

#logo {
  text-align: center;
}

.application {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: left;
  color: #2c3e50;
  min-height: 100vh;
  padding: 15px;
  background-color: #f5f5f5;

  border: 10px solid;
  border-image-source: linear-gradient(45deg, rgb(0,143,104), rgb(250,224,66));
  border-image-slice: 1;


}
div:hover {
   background-color: #f1f1f1;      
}

</style>



