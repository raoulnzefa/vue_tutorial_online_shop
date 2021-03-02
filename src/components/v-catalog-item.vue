<template>
 <div class="v-catalog-item">
   <img src="" alt="catalog img item">
   <p class="v-catalog-item__name">{{}}</p>
   <p class="v-catalog-item__price">price: 100</p>
   <button class="v-catalog-item__add_to_cart_btn btn">Add to card</button>
 </div>
</template>

<script>
export default {
name: "v-catalog-item",
  props: {
    product__data : {
      type: Object,
      default() {
        return {}
      }
    }
  },
}
</script>

<style lang="scss" scoped>
@import "../assets/styles/styles.scss";
  .v-catalog-item {
    flex-basis: 25%;
    box-shadow: 0 0 8px 0 #e0e0e0;
    padding: $padding*2;
    margin-bottom: $margin*2;
  }
</style>