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
    </div>
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

}

.user-input-wrapper {
  flex: 1;
}

.data-table-wrapper {
  flex: 4;
}

</style>