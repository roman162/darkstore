<template>
  <div
    class="popup__wrapper fadeOut"
    @click.stop="closePopup"
  >
    <div
      class="popup__container"
    >
      <form
        v-if="!formSended"
        class="popup"
      >
        <label
          class="popup__label"
        >
          Email*
          <input
            type="email"
            class="popup__input"
            placeholder="Email"
            required
            v-model="inputEmail"
          >
        </label>
        <span
          v-if="!emailIsValid && inputEmail.length > 1"
          class="error__message"
        >
          Введите корректный e-mail
        </span>
        <button
          type="submit"
          class="popup__button"
          @click.prevent="sendForm()"
        >
          Отправить
        </button>
      </form>
      <div
        class="popup__success"
        v-else
      >
        <div class="circle-loader">
          <div class="checkmark draw hide"></div>
        </div>
        <span class="popup__success-message">Спасибо</span>
      </div>
      <span
        class="popup__icon-close"
        @click.prevent="closePopup"
      >
      </span>
    </div>
  </div>
</template>

<script>
export default {
  data () {
    return {
      inputEmail: '',
      emailIsValid: true,
      formSended: false
    }
  },
  methods: {
    showPopup () {
      this.inputEmail = ''
      this.formSended = false
      const container = document.querySelector('.popup__wrapper')
      const popup = document.querySelector('.popup__container')
      container.classList.remove('fadeOut')
      container.classList.add('fadeIn')
      popup.classList.remove('fadeOut')
      popup.classList.add('fadeIn')
    },
    closePopup () {
      const container = document.querySelector('.popup__wrapper')
      const popup = document.querySelector('.popup__container')
      if (event.target === container || event.target === document.querySelector('.popup__icon-close')) {
        container.classList.add('fadeOut')
        container.classList.remove('fadeIn')
        popup.classList.add('fadeOut')
        popup.classList.remove('fadeIn')
      }
    },
    validateEmail () {
      return /^(.+)@(.+)\.(.+)$/.test(this.inputEmail)
    },
    successForm () {
      document.querySelector('.circle-loader').classList.add('load-complete')
      document.querySelector('.checkmark').classList.toggle('hide')
    },
    sendForm () {
      if(this.validateEmail()) {
        console.log(this.inputEmail)
        this.emailIsValid = true
        this.formSended = true
        let promise = new Promise((resolve) => {
          setTimeout(() => {
            resolve("result");
          }, 1000);
        });
        promise
          .then(
            () => {
              this.successForm()
            },
            () => {
              console.log('Ошибка отправки формы')
            }
          );
      } else {
        this.emailIsValid = false
      }
    }
  }
}
</script>

<style scoped lang="scss">
  .popup__wrapper{
    width: 100vw;
    height: 100vh;
    background-color: rgba(0, 0, 0, 0.2);
    position: fixed;
    top: 0;
    left: 0;
    z-index: 100;
    display: flex;
  }

  .popup__container{
    display: flex;
    position: relative;
    background: #fff;
    visibility: hidden;
    position: fixed;
    min-width: 400px;
    min-height: 120px;
    border-radius: 5px;
    top: 50%;
    left: 50%;
    box-shadow: 0 11px 15px -7px rgba(0,0,0,.2),
      0 24px 38px 3px rgba(0,0,0,.14),
      0 9px 46px 8px rgba(0,0,0,.12);
    transform: translate(-50%, -50%);
    z-index: 10;
  }

  .popup__success{
    flex-grow: 1;
    display: flex;
    flex-direction: column;
    align-items: center;
    padding: 20px;
  }

  .popup{
    flex-grow: 1;
    padding: 20px;
    display: flex;
    flex-direction: column;
    justify-content: space-between;
  }

  .error__message{
    font-size: 10px;
    color: red;
  }

  .fadeIn, .fadeOut {
    animation-duration: 0.4s;
    animation-timing-function: linear;
  }

  @keyframes fadeIn {
    from {
      opacity: 0;
      visibility: hidden;
    }
    to {
      opacity:1;
      visibility: visible;
    }
  }

  .fadeIn {
    animation-name: fadeIn;
    opacity: 1;
    visibility: visible;
  }

  @keyframes fadeOut {
    from {
      opacity: 1;
      visibility: visible;
    }
    to {
      opacity:0;
      visibility: hidden;
    }
  }

  .fadeOut {
    animation-name: fadeOut;
    opacity: 0;
    visibility: hidden;
  }

  .popup__label{
    display: flex;
    flex-direction: column;
    width: 100%;
  }

  .popup__input{
    padding: 10px;
    margin-top: 5px;

    &:hover,
    &:focus{
      border-color: #7DB945;
      box-shadow: none;
      outline: none;
    }
  }

  .popup__button{
    @include primary-button;
    padding: 10px;
    margin-top: 20px;
  }

  .popup__icon-close{
    position: absolute;
    top: 5px;
    right: 5px;
    display: flex;
    width: 30px;
    height: 30px;
    align-items: center;
    justify-content: center;
    cursor: pointer;
    background-image: url('../../assets/images/icon-close.svg');
    background-size: 50% 50%;
    background-position: 50% 50%;
    background-repeat: no-repeat;
  }

  $brand-success: #5cb85c;
  $loader-size: 50px;
  $check-height: $loader-size/2;
  $check-width: $check-height/2;
  $check-left: ($loader-size/6 + $loader-size/12);
  $check-thickness: 3px;
  $check-color: $brand-success;

  .circle-loader {
    margin-bottom: $loader-size/2;
    border: 1px solid rgba(0, 0, 0, 0.2);
    border-left-color: $check-color;
    animation: loader-spin 1.2s infinite linear;
    position: relative;
    display: inline-block;
    vertical-align: top;
    border-radius: 50%;
    width: $loader-size;
    height: $loader-size;
  }

  .load-complete {
    -webkit-animation: none;
    animation: none;
    border-color: $check-color;
    transition: border 500ms ease-out;
  }

  .hide{
    display: none;
  }

  .checkmark {
    
    &.draw:after {
      animation-duration: 800ms;
      animation-timing-function: ease;
      animation-name: checkmark;
      transform: scaleX(-1) rotate(135deg);
    }
    
    &:after {
      opacity: 1;
      height: $check-height;
      width: $check-width;
      transform-origin: left top;
      border-right: $check-thickness solid $check-color;
      border-top: $check-thickness solid $check-color;
      content: '';
      left: $check-left;
      top: $check-height;
      position: absolute;
    }
  }

  @keyframes loader-spin {
    0% {
      transform: rotate(0deg);
    }
    100% {
      transform: rotate(360deg);
    }
  }

  @keyframes checkmark {
    0% {
      height: 0;
      width: 0;
      opacity: 1;
    }
    20% {
      height: 0;
      width: $check-width;
      opacity: 1;
    }
    40% {
      height: $check-height;
      width: $check-width;
      opacity: 1;
    }
    100% {
      height: $check-height;
      width: $check-width;
      opacity: 1;
    }
  }
</style>
