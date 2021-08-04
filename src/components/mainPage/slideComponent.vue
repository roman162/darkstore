<template>
  <div class="slide">
    <img
      class="slide__image"
      :src="slide.image"
    >
    <h3 class="slide__title">
      {{ slide.title }}
    </h3>
    <span class="slide__description">
      {{ slide.description }}
    </span>
  </div>
</template>

<script>
export default {
  props: {
    slide: {
      type: Object
    }
  }
}
</script>

<style scoped lang="scss">
  .slide{
    padding: 40px;
    background-color: #fff;
    box-shadow: 0px 0px 40px rgba(0, 0, 0, 0.1);
    border-radius: 10px;
    text-align: center;
    font-size: 16px;
    line-height: 24px;
  }

  .slide__image{
    max-width: calc(100vw - 179px);
    width: 561px;
  }

  .slide__title{
    font-weight: bold;
  }
</style>