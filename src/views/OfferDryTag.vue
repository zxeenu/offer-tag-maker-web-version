/** 
This is the fist view. 
It consists of a data entry widget and a table weidget

The idea is for entrered data to go to a table with full CRUD functionalilty for the table
The data on the table will then be converted into a pdf

It will need a loading screen while the pdf is generated

*/

<template>
  <div>
    <UserInputTypeDry/> 
  </div>
</template>

<script>
import UserInputTypeDry from "../components/UserInputTypeDry";

export default {
  name: "OfferDryTag",
  components: { UserInputTypeDry }
}
</script>

<style scoped>

</style>