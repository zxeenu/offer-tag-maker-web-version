<template>
<div class="application-container">
  <div id="logo">
    <img alt="Vue logo" src="./assets/logo.png">
  </div>
  <div class="application">
    <div class="input-container"><OfferDryTag/></div> 
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

.application-container {

  background-color: #f5f5f5;
  border: 10px solid;
  border-image-source: linear-gradient(45deg, rgb(0,143,104), rgb(250,224,66));
  border-image-slice: 1;
  color: #2c3e50;
  margin-left: auto;
  margin-right: auto;
}

.application {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: left;
  min-height: 100vh;
  padding: 15px;
  display: flex;
  flex-direction: row;
  justify-content: flex-end;
  margin-right: auto;
}

.input-container {
  flex: 1;
}

div:hover {
   background-color: #EEF1f1;      
}

</style>



