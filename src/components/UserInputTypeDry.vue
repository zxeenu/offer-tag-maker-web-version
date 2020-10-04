/*
This is a component to create a little user interface to extract data through a form
 */

<template>
    <div class="user">
        <div class="user-data-entry">
            <form @submit.prevent="addDataToTable">
                <p><strong>Item Description</strong></p>
                <input class="item-details-textarea" v-model="itemDescriptionString"/>
                <p><strong>Normal Retail Price</strong></p>
                <input class="item-details-textarea" v-model="itemNormalRetailPriceString"/>
                <p><strong>Special Offer Price</strong></p>
                <input class="item-details-textarea" v-model="itemSpecialOfferPriceString"/>
                <p><strong>Packing</strong></p>
                <input class="item-details-textarea" v-model="itemPackingString"/>
                <p><strong>Item Expiry Date</strong></p>
                <input class="item-details-textarea" v-model="itemExpiryDateString"/>
                <p></p>
                <button class="item-details-textarea">Next</button>
                <p></p>
            </form>

            <form @submit.prevent="createPDFFromDataTable">
                <button class="item-print-button">Create PDF</button>
            </form>
        </div>



    </div>
</template>

<script>
export default {
    name: "UserInputTypeDry",
    
    data() {
        return {
            itemDescriptionString: "",
            itemNormalRetailPriceString: "",
            itemSpecialOfferPriceString: "",
            itemPackingString: "",
            itemExpiryDateString: "",
            priceTagList: [
                {
                    name: "",
                    retailPrice: "",
                    offerPrice: "",
                    packing: "",
                    expiryDate:""
                }
            ]

        }
    },
    watch: {
        itemDescriptionString: function(val) {
            if (val.length > 40) {
                this.itemDescriptionString = val.substr(0, 40);
                console.log(val.length)
            }
        },
        itemNormalRetailPriceString: function(val) {
            if (val.length > 7) {
                this.itemNormalRetailPriceString = val.substr(0, 7);
                console.log(val.length)
            }
        },
        itemSpecialOfferPriceString: function(val) {
            if (val.length > 7) {
                this.itemSpecialOfferPriceString = val.substr(0, 7);
                console.log(val.length)
            }
        },
        itemPackingString: function(val) {
            if (val.length > 10) {
                this.itemPackingString = val.substr(0, 10);
                console.log(val.length)
            }
        },
        itemExpiryDateString: function(val) {
            if (val.length > 17) {
                this.itemExpiryDateString = val.substr(0, 17);
                console.log(val.length)
            }
        }
    }


}

// a mechanism for taking the user input, trimming the white spaces, and putting it
// inside an array object has to be implemented

</script>

<style scoped>

.user {
  display: grid;
  grid-template-columns: 1fr 3fr;
  padding: 50px 10%;
}

.user-data-entry {
    display: flex;
    flex-direction: column;
    margin-right: 50px;
    padding: 20px;
    background-color: white;
    border-radius: 5px;
    border: 1px solid #dfe3df;
    min-width: 300px;
    text-align: center;
}

.item-details-textarea {
    resize: none;
    min-width: 300px;
}

.item-print-button {
    min-width: 300px;
}

</style>