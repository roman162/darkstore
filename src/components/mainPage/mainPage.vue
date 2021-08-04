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
  .main-page{
    font-family: Rotonda, sans-serif;
  }

  .buy-button{
    @include primary-button;
    padding: 20px;
    min-width: 340px;
    margin: 0 auto;
    font-size: 22px;
    font-weight: bold;
  }
</style>