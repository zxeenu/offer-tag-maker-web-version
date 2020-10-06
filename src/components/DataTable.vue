<template>
  <div>
      <p v-for="(tagData, index) in tagDataList" :key="index">
          {{ tagData.name }} | {{ tagData.retailPrice }} | {{ tagData.offerPrice }} | {{ tagData.packing }} | {{ tagData.expiry }}
      </p>
  </div>
</template>

<script>

/**
 * The prop is used to connect the array of objects which hold the data fro the table from the UserInputTypeDry component
 */
export default {
    name: "DataTable",
    props: {
        tagDataList: {
            type: Object,
            required: true
        }
    }

}
</script>

<style>

</style>