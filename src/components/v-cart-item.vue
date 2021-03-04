<template>
  <div class="v-cart-item">
    <img src="require('../assets/images/' + cart_item_data.image)" alt="image">
    <div class="v-cart-info"></div>
    <p>{{cart_item_data.name}}</p>
    <p>{{cart_item_data.price}}</p>
    <p>{{cart_item_data.article}}</p>
  </div>
</template>

<script>
export default {
  name: "v-card-item",
  props: {
    cart_item_data: {
      type: Object,
      default(){
        return {}
      }
    }
  },
}
</script>

<style scoped>

</style>