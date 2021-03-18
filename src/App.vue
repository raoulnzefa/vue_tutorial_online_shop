<template>
  <div id="app">
  <v-main-wrapper/>
  </div>
</template>

<script>

import vMainWrapper from './components/v-main-wrapper'
import {mapActions, mapGetters} from 'vuex'
export default {
  name: "app",
  components: {
    vMainWrapper
  },
  computed: {
    ...mapGetters([
        'IS_MOBILE',
        'IS_DESKTOP'
    ])
  },
  methods: {
    ...mapActions([
      'SET_DESKTOP',
      'SET_MOBILE'
    ]),
  },
  mounted() {
    let vm = this
    window.addEventListener('resize', ()=> {
      if(window.innerWidth > 767) {
        // this.$store.dispatch('SET_DESKTOP')
        vm.SET_DESKTOP()
        console.log('Desktop', vm.IS_DESKTOP)
      }else {
        // this.$store.dispatch('SET_MOBILE')
        vm.SET_MOBILE()
        console.log('Mobile', vm.IS_MOBILE)
      }
    })
  }
}
</script>

<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 160px;
}

</style>
