<template>
  <div class="slider">
    <h2 class="slider__title">Взгляните на процесс сборки своими глазами</h2>
    <div class="slider__container">
      <span
        class="slider__control slider__control--prev"
        :class="currentSlide === 0 ? 'slider__control--disabled' : ''"
        @click="translateSlider(-1)"
      />
      <span
        class="slider__control slider__control--next"
        :class="currentSlide === slides.length - 1 ? 'slider__control--disabled' : ''"
        @click="translateSlider(1)"
      />
      <ul class="slider__list">
        <li
          class="slider__item"
          v-for="(slide, index) of slides"
          :key="index"
        >
          <slide-component
            :slide="slide"
          />
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
import slideComponent from '../mainPage/slideComponent.vue';
export default {
  components: {
    slideComponent,
  },
  data () {
    return {
      slides: [
        {
          title: 'Привезем точно по списку',
          description: 'Сборщик берëт с собой наручный терминал, на котором он видит весь список покупок для каждого заказа.',
          image: require('@/assets/images/image1.jpg')
        },
        {
          title: 'Собираем быстро и эффективно',
          description: 'Для улучшения эргономики пространства товары размещены от тяжëлых к лëгким, находящимся уже в конечной зоне упаковки.',
          image: require('@/assets/images/image2.jpg')
        },
        {
          title: 'За свежесть и качество отвечаем',
          description: 'Выделены специальные зоны, в том числе холодная и морозильная. ',
          image: require('@/assets/images/image3.jpg')
        },
        {
          title: 'Шампунь не положат рядом с рыбой',
          description: 'Собираем и упаковываем ваш заказ с заботой: соблюдаем принципы товарного соседства и учитываем вес товара.',
          image: require('@/assets/images/image4.jpg')
        },
        {
          title: 'Довезëм в сохранности даже яйца',
          description: 'Бережно транспортируем контейнеры, фиксируя их стяжными ремнями. Системы охлаждения поддерживают температурный режим.',
          image: require('@/assets/images/image5.jpg')
        },
      ],
      currentSlide: 0
    }
  },
  methods: {
    translateSlider (value) {
      const slider = document.querySelector('.slider__list')
      const slideWidth = document.querySelector('.slider__item').offsetWidth
      let slideIndex = this.currentSlide + value
      if (slideIndex < 0) {
        slideIndex = 0
      } else if (slideIndex > this.slides.length - 1) {
        slideIndex = this.slides.length - 1
      }
      this.currentSlide = slideIndex
      slider.style.left = -(this.currentSlide * (slideWidth + 100)) + 50 + 'px'
    }
  },
}
</script>

<style scoped lang="scss">
  .slider__title{
    text-align: center;
  }

  .slider__list{
    display: flex;
    margin: 0;
    padding: 0;
    position: relative;
    left: 50px;
    transition: 1s;
  }

  .slider__item{
    list-style: none;
    display: flex;
    align-items: stretch;
    margin-right: 100px;
    
    &:last-child{
      margin-right: 0;
    }
  }

  .slider__container{
    margin: 0 auto;
    padding: 50px 0;
    overflow: hidden;
    max-width: 730px;
    width: 100%;
    position: relative;
  }

  .slider__control{
    position: absolute;
    width: 20px;
    height: 20px;
    border-left: 3px solid #D0D5CD;
    border-bottom: 3px solid #D0D5CD;
    top: calc(50% - 16px);
    cursor: pointer;
    z-index: 10;

    &:hover{
      border-color: #babdb9;
    }

    &--prev{
      transform: rotate(45deg);
      left: 15px;
    }

    &--next{
      transform: rotate(225deg);
      right: 5px;
    }

    &--disabled{
      opacity: 0.5;

      &:hover{
        border-color: #D0D5CD;
      }
    }
  }
</style>