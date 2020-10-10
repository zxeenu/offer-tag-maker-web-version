/** 
This is the fist view. 
It consists of a data entry widget and a table weidget

The idea is for entrered data to go to a table with full CRUD functionalilty for the table
The data on the table will then be converted into a pdf

It will need a loading screen while the pdf is generated

*/

<template>
  <div class="container-wrapper">
    <div class="user-input-wrapper">
      <UserInputTypeDry @price-list="connectionAcrossComponents"/> 
      <!-- <form @submit.prevent="test">
        <button >test - empty list</button>
      </form>
      <form @submit.prevent="test2">
        <button >test - print list</button>
      </form> -->
    </div>
    <!-- <div class="data-table-wrapper">
      <DataTable :tagDataList="priceTagList_" />
    </div> -->
  </div>
  
  <div class="data-table-wrapper">
    <DataTable :tagDataList="priceTagList_" @price-tag-to-delete="deleteFromTagList"/>
  </div>


  

</template>

<script>
import UserInputTypeDry from "../components/UserInputTypeDry";
import DataTable from "../components/DataTable";

export default {
  name: "OfferDryTag",
  components: { UserInputTypeDry, DataTable },
  data() {
    return {
      priceTagList_: []
    }
  },
  methods: {
    connectionAcrossComponents(priceTagList) {
      // connects the priceTagList array to the priceTagList_ array
      this.priceTagList_ = priceTagList;
    },
    deleteFromTagList(tagDataSelected) {
      // this.priceTagList_ = this.priceTagList_.filter(x => x.id !== tagDataSelected.id); 
      // filter doesnt work, as after deleting with filer, the object reference is lost, and we cant add new items to the list
      var removeIndex = this.priceTagList_.map(item => item.id)
                       .indexOf(tagDataSelected.id);

      ~removeIndex && this.priceTagList_.splice(removeIndex, 1);
    },
    test() {
      this.priceTagList_.length = 0;
    },
    test2() {
      this.priceTagList_.forEach(function (obj) {
        console.log(obj.name + obj.retailPrice + obj.offerPrice + obj.packing + obj.expiryDate + obj.id);
      })
    }
  },
  mounted() {

  }
}
</script>

<style scoped>

.container-wrapper {
  padding: 15px;
  display: flex;
  flex-direction: row;
  justify-content: flex-end;
  /* margin-right: auto;
  height: 100%; */

}

.user-input-wrapper {
  /* border: 10px solid;
  border-image-source: linear-gradient(45deg, rgb(0,143,104), rgb(250,224,66));
  border-image-slice: 1;
  color: #2c3e50; */
  flex: 1;
  /* height: 100%;
  position: relative; */
}

.data-table-wrapper {
  /* border: 10px solid;
  border-image-source: linear-gradient(45deg, rgb(0,143,104), rgb(250,224,66));
  border-image-slice: 1;
  color: #2c3e50; */
  flex: 4;
  /* height: 100%;
  position: relative; */
}

</style>