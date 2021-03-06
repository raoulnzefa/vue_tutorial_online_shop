<template>
  <div class="v-catalog">
    <router-link :to="{name: 'cart', params: {cart_data: CART}}">
      <div class="v-catalog__link_to_cart">Cart: {{CART.length}}</div>
    </router-link>
    <h1>Catalog</h1>
    <v-select
      :options="options"
      @select="optionSelect"
      :selected="selected"
    />
    <div class="v-catalog__list">
      <v-catalog-item
          v-for="(product, i) in PRODUCTS"
          :key="i"
          :product__data="product"
          @addToCart="addToCart"

      />
      <p>Selected option goes here: {{selected}}</p>
    </div>
  </div>
</template>

<script>
import vCatalogItem from './v-catalog-item'
import vSelect from '../v-select'
import {mapActions, mapGetters} from 'vuex'
export default {
  name: "v-catalog",
  components: {
    vCatalogItem,
    vSelect
  },
  data() {
    return {
      options:
          [
            {name : 'option 1', value: 1},
            {name : 'option 2', value: 2},
            {name : 'option 3', value: 3},
            {name : 'option 4', value: 4},
            {name : 'option 5', value: 5}
          ],
      selected: 'Select',
    }
  },
  methods: {
    ...mapActions([
        'GET_PRODUCTS_FROM_API',
        'ADD_TO_CART'
    ]),
    addToCart(data) {
      this.ADD_TO_CART(data)
    },
    optionSelect(option) {
      this.selected = option.name
    }
  },
  mounted() {
    this.GET_PRODUCTS_FROM_API()
    .then((response)=> {
      if(response.data) {
        console.log("Data arrived")
      }
    })
  },
  computed: {
    ...mapGetters([
      'PRODUCTS',
        'CART'
    ])
  }
}
</script>

<style lang="scss" scoped>
@import "../../assets/styles/styles";
  .v-catalog {
    &__list {
      display: flex;
      flex-wrap: wrap;
      justify-content: space-between;
      align-items: center;
    }
    &__link_to_cart {
      position: absolute;
      top: 10px;
      right: 10px;
      padding: $padding*2;
      border: 1px solid #aeaeae;
      border-radius: 10px;
    }
  }
</style>