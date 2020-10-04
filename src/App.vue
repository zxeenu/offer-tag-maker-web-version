<template>
  <div id="logo">
    <img alt="Vue logo" src="./assets/logo.png">
  </div>
  <div id="app">
    <OfferDryTag/> 
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

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: left;
  color: #2c3e50;
  min-height: 100vh;
  background-color: #F3F5FA;
}
</style>



