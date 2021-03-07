<template>
  <div class="v-select">
    <p
        class="title"
        @click="arrOptionsVisible = !arrOptionsVisible"
    >{{selected}}</p>
    <div class="options"
      v-if="arrOptionsVisible || isExpanded"
    >
      <p
          v-for="option in options"
          :key="option.value"
          @click="selectOption(option)"
      >
        {{option.name}}
      </p>
    </div>
  </div>
</template>

<script>
export default {
  name: "v-select",
  props: {
    options: {
      type: Array,
      default() {
        return []
      }
    },
    selected: {
      type: String,
      default: ''
    },
    isExpanded: {
      type: Boolean,
      default: false
    },
  },
  data(){
    return  {
      arrOptionsVisible: false
    }
  },
  methods: {
    selectOption(option) {
      this.$emit('select', option)
      this.arrOptionsVisible = false
    },
    hideSelected() {
      this.arrOptionsVisible = false
    }
  },
  mounted() {
    document.addEventListener('click', this.hideSelected.bind(this), true)
  },
  beforeDestroy() {
    document.removeEventListener('click', this.hideSelected)
  },
}
</script>

<style lang="scss" scoped>
  .v-select {
    position: relative;
    width: 200px;
    cursor: pointer;
    p {
      margin: 0;
    }
    .options {
      border: 1px solid #aeaeae;
      position: absolute;
      top: 30px;
      right: 0;
      width: 100%;
      p{
        &:hover {
          background: #e7e7e7;
        }
      }
    }
    .title {
      border: 1px solid #aeaeae;
    }
  }
</style>