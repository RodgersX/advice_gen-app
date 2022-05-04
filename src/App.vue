<template>
  <v-app id="app">
    <div class="advice-card">
      <p class="advice-title">ADVICE #{{ advice.id }}</p>
      <p class="advice-text">
        <i class="bx bxs-quote-left"></i>
        {{ advice.data }}
        <i class="bx bxs-quote-right"></i>
        </p>
      <div class="d-flex align-center divider">
        <v-img
          :src="require('./assets/pattern-divider-mobile.svg')"
          alt="divider"
        />
      </div>
      <button @click.stop="loadAdvice" class="refresh-btn">
        <v-img :src="require('./assets/icon-dice.svg')" alt="dice"></v-img>
      </button>
    </div>
  </v-app>
</template>

<script>
import axios from "axios";

export default {
  data() {
    return {
      advice: {
        data: null,
        id: null,
      },
    };
  },

  mounted() {
    this.loadAdvice();
  },

  methods: {
    async loadAdvice() {
      let advice = await axios.get("https://api.adviceslip.com/advice");
      if (advice) {
        this.advice.data = advice.data.slip.advice;
        this.advice.id = advice.data.slip.id;
      }
    },
  },
};
</script>

<style scoped lang="sass">
#app
 width: 100vw
 height: 100vh
 background-color: hsl(218, 23%, 16%)

.advice-card
  background-color: hsl(217, 19%, 24%)
  border-radius: 10px
  color: white
  text-align: center
  padding: 40px
  box-shadow: 10px 10px 20px hsl(218, 23%, 16%)
  min-width: 300px
  width: 80%
  min-height: 300px
  margin: auto
  position: relative
  font-family: 'Epilogue', sans-serif
  font-family: 'Manrope', sans-serif
  font-family: 'Mulish', sans-serif
  font-family: 'Poppins', sans-serif

.refresh-btn
  background-color: hsl(150, 80%, 60%)
  display: flex
  align-items: center
  justify-content: center
  width: 60px
  padding: 15px
  height: 60px
  border-radius: 50%
  position: absolute
  left: 50%
  top: 102%
  transform: translate(-50%, -60%)


.refresh-btn:hover,
.refresh-btn:active
  background-color: hsl(150, 100%, 60%)
  box-shadow: 0 2px 30px 1px hsl(150, 100%, 60%)

.divider
  margin-bottom: 20px

.advice-title
  color: hsl(150, 100%, 66%)
  font-size: 15px

.advice-text
  font-size: 28px
  font-weight: 800
</style>
