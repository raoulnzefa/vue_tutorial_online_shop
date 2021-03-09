<template>
  <div class="popup_wrapper"ref="popupWrapper">
    <div class="v-popup">
      <div class="v-popup__header">
        <span>{{popupTitle}}</span>
        <span>
        <i
            class="material-icons"
            @click="closePopup"
        >
          close
        </i>
      </span>
      </div>
      <div class="v-popup__content">
        <slot></slot>
      </div>
      <div class="v-popup__footer">
        <button
            class="close_modal"
            @click="closePopup"
        >
          Close
        </button>
        <button class="submit_btn"
                @click="rightBtnAction"
        >
          {{rightBtnTitle}}
        </button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "v-popup",
  methods: {
    closePopup() {
      this.$emit('closePopup')
    },
    rightBtnAction() {
      this.$emit('rightBtnAction')
    }
  },
  props: {
    rightBtnTitle: {
      type: String,
      default: 'OK'
    },
    popupTitle: {
      type: String,
      default: 'Popup name'
    }
  },
  mounted() {
    let vm = this;
    document.addEventListener('click', (item)=> {
      if(item.target === vm.$refs['popupWrapper']) {
        vm.closePopup()
      }
    })
  }
}
</script>

<style lang="scss" scoped>
  .popup_wrapper {
    background: rgba(64,64,64,.4);
    display: flex;
    justify-content: center;
    align-items: center;
    position: absolute;
    right: 0;
    left: 0;
    top: 0;
    bottom: 0;
  }
  .v-popup {
    padding: 16px;
    position: fixed;
    top: 50px;
    width: 400px;
    background: #fff;
    box-shadow: 0 0 17px #e7e7e7;
    z-index: 3;
    &__header, &__footer {
      display: flex;
      justify-content: space-between;
      align-items: center;
    }
    &__content {
      display: flex;
      justify-content: center;
      align-items: center;
    }
    .submit_btn {
      padding: 8px;
      color: #fff;
      background: #26ae68;
      cursor: pointer;
    }
    .close_modal {
      padding: 8px;
      background: red;
      color: #fff;
      cursor: pointer;
    }
    .material-icons {
      cursor: pointer;
    }
  }
</style>