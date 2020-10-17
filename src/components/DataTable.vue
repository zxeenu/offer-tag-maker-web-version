<template>
  <div v-if="tagDataList.length >= 1">
        <div class="flex-table-heading">
            <div><strong>ITEM NAME</strong></div>
            <div><strong>RETAIL PRICE</strong></div>
            <div><strong>OFFER PRICE</strong></div>
            <div><strong>PACKING</strong></div>
            <div><strong>EXPIRY DATE</strong></div>
        </div>
        <div v-for="(tagData, index) in tagDataList" :key="index" class="flex-table">
            <div>{{ tagData.name }}</div>
            <div>{{ tagData.retailPrice }}</div>
            <div>{{ tagData.offerPrice }}</div>
            <div>{{ tagData.packing }}</div>
            <div>{{ tagData.expiryDate }}</div>
          <div><form @submit.prevent="deleteItem(tagData)"><button>Delete</button></form></div>
        </div>
  </div>
</template>

<script>

/**
 * The prop is used to connect the array of objects which hold the data fro the table from the UserInputTypeDry component
 */
export default {
    name: "DataTable",
    emits: ["price-tag-to-delete"],
    props: {
        tagDataList: {
            type: Object,
            required: true
        }
    },
    methods: {
        deleteItem(tagDataSelected) {
            this.$emit("price-tag-to-delete", tagDataSelected);
        }

            
    }

}
</script>

<style lang="scss" scoped>

.flex-table {
    display: grid;
    grid-template-columns: repeat(auto-fill, 18%);
    grid-template-rows: repeat(auto-fill, 14%);
    overflow-wrap: break-word;
    font-size: 90%;
    padding: 10px;
    border-bottom: 1px black solid;

    &:nth-of-type(2n) {
        background-color: #dedede;
    }

    .actions {
        * {
            padding-right: 15px;
        }
    }

}

.flex-table-heading {
    display: grid;
    font-size: 100%;
    grid-template-columns: repeat(auto-fill, 18%);
    grid-template-rows: repeat(auto-fill, 14%);
    padding: 10px;
    border-bottom: 1px black solid;

}

</style>