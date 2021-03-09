<template>
 <div class="v-catalog-item">

   <v-popup
    v-if="isInfoPopupVisible"
    @closePopup='closeInfoPopup'
    rightBtnTitle = 'Add to cart'
    :popup-title="product__data.name"
    @rightBtnAction="addToCart"
   >
     <img class="v-catalog-item__image" :src=" require('../../assets/images/' + product__data.image)" alt="catalog img item">
     <div>
       <p class="v-catalog-item__name">{{product__data.name}}</p>
       <p class="v-catalog-item__price">price: {{product__data.price | toFix | formattedPrice}}</p>
       <p class="v-catalog-item__price">{{product__data.category}}</p>
     </div>
   </v-popup>

   <img class="v-catalog-item__image" :src=" require('../../assets/images/' + product__data.image)" alt="catalog img item">
   <p class="v-catalog-item__name">{{product__data.name}}</p>
   <p class="v-catalog-item__price">price: {{product__data.price | toFix | formattedPrice}}</p>
   <button
       class="v-catalog-item__show-ifo"
       @click="showPopupInfo"
   >
     Show info
   </button>
   <button
       class="v-catalog-item__add_to_cart_btn btn"
       @click="addToCart"
   >Add to card
   </button>
 </div>
</template>

<script>
import vPopup from '../popup/v-popup'
import toFix from "@/components/filters/toFix";
import formattedPrice from "@/components/filters/price-format";
export default {
name: "v-catalog-item",
  components: {
    vPopup
  },
  props: {
    product__data : {
      type: Object,
      default() {
        return {}
      }
    }
  },
  methods: {
    addToCart() {
      this.$emit('addToCart', this.product__data)
    },
    showPopupInfo() {
      this.isInfoPopupVisible = true
    },
    closeInfoPopup() {
      this.isInfoPopupVisible = false
    }
  },
  mounted() {
    this.$set(this.product__data, 'quantity', 1)
  },
  data() {
    return {
      isInfoPopupVisible: false
    }
  },
  filters: {
    toFix,
    formattedPrice
  }
}
</script>

<style lang="scss" scoped>
@import "../../assets/styles/styles";
  .v-catalog-item {
    flex-basis: 25%;
    box-shadow: 0 0 8px 0 #e0e0e0;
    padding: $padding*2;
    margin-bottom: $margin*2;
    &__image {
      max-width: 100px;
      width: 100%;
      object-fit: cover;
    }
  }
</style>