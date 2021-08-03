<template>
  <main class="main-page">
    <default-slider />
    <Popup
      ref="popup"
    />
    <button
      class="buy-button"
      @click="showPopup"
    >
      Купить
    </button>
  </main>
</template>

<script>
import defaultSlider from '../mainPage/defaultSlider.vue'
import Popup from '../mainPage/Popup.vue'

export default {
  name: 'mainPage',
  components: {
    defaultSlider,
    Popup
  },
  methods: {
    showPopup () {
      this.$refs.popup.showPopup()
    }
  }
}
</script>

<style scoped lang="scss">
  .buy-button{
    outline: none;
    border: none;
    background-color: initial;
    padding: 20px;
    background: linear-gradient(0deg, #7DB945, #7DB945), #7DB945;
    color: #fff;
    font-weight: bold;
    border-radius: 10px;
    text-transform: uppercase;
    min-width: 340px;
    cursor: pointer;
    display: block;
    margin: 0 auto;
  }
</style>