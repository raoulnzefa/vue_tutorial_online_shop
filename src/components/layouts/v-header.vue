<template>
  <div class="v-header">
    <router-link :to="{name: 'mainPage'}">
      <img src="../../assets/logo.png" alt="logo">
    </router-link>

    <div class="search-field">
      <input
          type="text"
          v-model="searchValue"
      >
      <button class="search-btn">
        <i class="material-icons">search</i>
      </button>
    </div>

  </div>
</template>

<script>
export default {
  name: "v-headers",
  data() {
    return {
      searchValue: ''
    }
  }
}
</script>

<style lang="scss" scoped>
@import "../../assets/styles/virebles";
  .v-header {
    display: flex;
    justify-content: space-between;
    align-items: center;
    background: $green-bg;
    padding: 16px;
    width: 100%;
    position: fixed;
    left: 0;
    top: 0;
    img {
      width: 50px;
    }
    .search-field {
      padding: 16px;
      position: relative;
      right: 200px;
      display: flex;
      justify-content: center;
      align-items: center;
      .search-btn {
        margin-left: 16px;
        background: transparent;
        border: none;
        outline: none;
      }
    }
  }
</style>