<template>
  <div class="v-catalog">
    <router-link :to="{name: 'cart', params: {cart_data: CART}}">
      <div class="v-catalog__link_to_cart">Cart: {{CART.length}}</div>
    </router-link>
    <h1>Catalog</h1>
    <v-select
      :options="categories"
      @select="sortByCaegories"
      :selected="selected"
    />
    <div class="v-catalog__list">
      <v-catalog-item
          v-for="(product, i) in filteredProducts"
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
      categories:
          [
            {name : 'Все', value: 'All'},
            {name : 'Мужские', value: 'м'},
            {name: 'Женские', value: 'ж'}
          ],
      selected: 'Все',
      sortedProducts: []
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
    sortByCaegories(option) {
      this.sortedProducts = []
      let vm = this
      this.PRODUCTS.map((item)=> {
        if(item.category === option.name) {
          vm.sortedProducts.push(item)
        }
      })
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
    ]),
    filteredProducts() {
      if(this.sortedProducts.length) {
        return this.sortedProducts
      }else {
        return this.PRODUCTS
      }
    }
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