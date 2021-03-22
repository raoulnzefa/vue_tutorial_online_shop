<template>
  <div class="v-header">
    <router-link :to="{name: 'mainPage'}">
      <img src="../../assets/logo.png" alt="logo">
    </router-link>

    <div class="search-field">
      <div class="input-wrapper">
        <input
            type="text"
            v-model="searchValue"
            maxlength="20"
        >
        <i class="material-icons" @click="search(searchValue)">search</i>
      </div>
      <button class="search-btn">
        <i class="material-icons" @click="clearSearchField">
          cancel
        </i>
      </button>
    </div>

  </div>
</template>

<script>
import {mapActions, mapGetters} from 'vuex'
export default {
  name: "v-headers",
  data() {
    return {
      searchValue: ''
    }
  },
  computed: {
    ...mapGetters([
      'SEARCH_VALUES'
    ])
  },
  methods: {
    ...mapActions([
      'GET_SEARCH_VALUE_TO_VUEX'
    ]),
    search(value) {
      this.GET_SEARCH_VALUE_TO_VUEX(value)
      if(this.$route.path !== '/catalog') {
        this.$router.push('/catalog')
      }
    },
    clearSearchField() {
      this.searchValue = ''
      this.GET_SEARCH_VALUE_TO_VUEX()
      if(this.$route.path !== '/catalog') {
        this.$router.push('/catalog')
      }
    },
  },
}
</script>

<style lang="scss" scoped>
@import "../../assets/styles/virebles";
  .v-header {
    display: flex;
    justify-content: space-between;
    align-items: center;
    background: $green-bg;
    padding: 16px 0 16px 16px;
    width: 100%;
    img {
      width: 50px;
    }
    .search-field {
      padding: 16px;
      position: relative;
      display: flex;
      justify-content: center;
      align-items: center;
      .search-btn {
        display: flex;
        background: transparent;
        border: none;
        outline: none;
      }
      .input-wrapper {
        display: flex;
        position: relative;
        .material-icons {
          position: absolute;
          right: 0;
          &:hover {
            cursor: pointer;
          }
        }
        input {
          outline: none;
          border: none;
          border-radius: 3px;
          height: 24px;
          padding-left: 5px;
        }
      }
    }
  }
</style>