<template>
  <v-app id="app">
    <div class="advice-card">
      <p class="advice-title">ADVICE #{{ advice.id }}</p>
      <p class="advice-text">"{{ advice.data }}"</p>
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
  padding: 4rem
  max-width: 80%
  min-width: 50%
  min-height: 300px
  margin: auto
  position: relative
  font-family: 'Epilogue', sans-serif
  font-family: 'Manrope', sans-serif
  font-family: 'Mulish', sans-serif
  font-family: 'Poppins', sans-serif

.refresh-btn
  position: absolute
  bottom: -10%
  right: 47%
  border-radius: 27px
  padding: 1rem
  background-color: hsl(150, 80%, 60%)

.refresh-btn:hover,
.refresh-btn:active
  background-color: hsl(150, 100%, 60%)
  box-shadow: 0 2px 30px 1px hsl(150, 100%, 60%)

.divider
  margin-top: 4rem

.advice-title
  color: hsl(150, 100%, 66%)
  font-size: 15px

.advice-text
  font-size: 28px
  font-weight: 800
</style>
