<template>
  <div class="v-main-wrapper">
<!--    <p>{{title}}</p>-->
    <v-catalog/>
    <v-card
        v-if="CART.length"
        :cart_data="CART"
    />
  </div>
</template>

<script>
import vCatalog from './v-catalog'
import vCard from './v-cart'
import {mapGetters} from 'vuex'
export default {
  name: "v-main-wrapper.vue",
  components: {
    vCatalog,
    vCard
},
  props: {},
  data() {
    return {
      title :"Main"
    }
  },
  computed: {
    ...mapGetters([
        'CART'
    ])
  },
  methods: {},
  watch: {},
  mounted() {
    console.log('Hello i am alive')
  }
}
</script>

<style scoped>
.v-main-wrapper {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  max-width: 900px;
  margin: 0 auto;
}
</style>