<template>
  <div class="v-cad">
    <h2>Cart</h2>
    <v-cart-item/>
  </div>
</template>

<script>
import vCartItem from './v-cart-item'
export default {
  name: "v-card",
  components: {
    vCartItem
  },
  props: {
    cart_data: {
      type: Array,
      default() {
        return [];
      }
    }
  },
}
</script>

<style scoped>

</style>