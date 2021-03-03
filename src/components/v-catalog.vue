<template>
  <div class="v-catalog">
    <h1>catalog</h1>
    <div class="v-catalog__list">
      <v-catalog-item
          v-for="product in PRODUCTS"
          :key="product.article"
          :product__data="product"
          @sendDataToParent="showChildArticleInConsole"
      />
    </div>
  </div>
</template>

<script>
import vCatalogItem from  './v-catalog-item'
import {mapActions, mapGetters} from 'vuex'
export default {
  name: "v-catalog",
  components: {
    vCatalogItem
  },
  data() {
    return {

    }
  },
  methods: {
    ...mapActions([
        'GET_PRODUCTS_FROM_API'
    ]),
    showChildArticleInConsole(data) {
      console.log(data)
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
      'PRODUCTS'
    ])
  }
}
</script>

<style lang="scss" scoped>
  .v-catalog {
    &__list {
      display: flex;
      flex-wrap: wrap;
      justify-content: space-between;
      align-items: center;
    }
  }
</style>