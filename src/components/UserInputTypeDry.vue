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
        </div>
    </div>
    <div class="user">
        <div class="user-data-submit">
            <form @submit.prevent="createPDFFromDataTable">
                <!-- <div v-if="loadingIndicator"> <Circle></Circle> </div> -->
                <button class="item-print-button">Create PDF</button>
            </form>
            <p></p>
            <form @submit.prevent="clearDataFromTable">
                <button class="item-print-button">Clear Table</button>
            </form>
        </div>
    </div>
</template>

<script>

import * as pdfz from '../assets/PdfLogic';
// import {Circle} from 'vue-loading-spinner';

export default {
    name: "UserInputTypeDry",
    emits: ["price-list"],
    data() {
        return {
            itemDescriptionString: "",
            itemNormalRetailPriceString: "",
            itemSpecialOfferPriceString: "",
            itemPackingString: "",
            itemExpiryDateString: "",
            priceTagList: []
            // loadingIndicator: false
        }
    },
    components: {
        // Circle
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
    }, 
    methods: {
        addDataToTable() {
            // get data from the user input box
            let name = this.itemDescriptionString;
            let retailPrice = this.itemNormalRetailPriceString;
            let offerPrice = this.itemSpecialOfferPriceString;
            let packing = this.itemPackingString;
            let expiry = this.itemExpiryDateString;

            // only proceed to cleaning up the data if all text fields have been used
            if(name && retailPrice && offerPrice && packing && expiry) {

                // remove the white space form the front and the end of the string
                name = name.trim();
                retailPrice = retailPrice.trim();
                offerPrice = offerPrice.trim();
                packing = packing.trim();
                expiry = expiry.trim();


                // if only . decimal is there, add 00
                const regex_three = /[.]$/
                let testRetail_three = regex_three.test(retailPrice);
                let testOffer_three = regex_three.test(offerPrice);
                if (testRetail_three) {
                    retailPrice += "00";
                }
                if (testOffer_three) {
                    offerPrice += "00";
                }

                // if with decimals missing from the prices add them
                const regex_one = /^((?![.]).)*$/
                let testRetail_one = regex_one.test(retailPrice);
                let testOffer_one = regex_one.test(offerPrice);

                if (testRetail_one) {
                    retailPrice += ".00";
                }
                if (testOffer_one) {
                    offerPrice += ".00";
                }

                // if only 1 decimal is there
                



                // push the cleaned data into the array of pricelist objects
                this.priceTagList.push(
                    {
                        id: this.priceTagList.length + 1,
                        name: name,
                        retailPrice: retailPrice,
                        offerPrice: offerPrice,
                        packing: packing,
                        expiryDate: expiry
                    }
                )

                // remove the user input and prepare the ui for the next price tag object
                this.itemDescriptionString = "";
                this.itemNormalRetailPriceString = "";
                this.itemSpecialOfferPriceString = "";
                this.itemPackingString = "";
                this.itemExpiryDateString = "";
            } else {
                window.alert("Hi, you didn't fill out all the input boxes! 😢");
            }

        },
        createPDFFromDataTable() {
            if (this.priceTagList.length >= 1) {
                // this.loadingIndicator = true;
                pdfz.tag_maker_vue(this.priceTagList);
                // this.loadingIndicator = false;
            } else {
               window.alert("Hi, you need some data before you can create the PDF! 🤔");
            }
        }, 
        clearDataFromTable() {
            if (this.priceTagList.length >= 1) {
                this.priceTagList.length = 0;
            } else {
               window.alert("Hi, you need some data before you clear the table! 🤔");
            }
            
        }

    },
    mounted() {
        this.$emit("price-list", this.priceTagList);

    }


}

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

.user-data-submit {
    position:relative; 
    top:-90px;
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

</style>