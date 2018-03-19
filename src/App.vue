<template lang="pug">
  div#app
    // Pass a reactive int as the current step
    hot-stepper(
      :steps="steps",
      :c-step="cStep"
    )
    // Debug controller
    div#debug
      select(
        v-model="cStep"
      )
        option(
          v-for="(step, index) in steps",
          :key="index",
          :value="index"
        ) {{step}}
      button(
        @click="goBack"
      )
        span BACK
      span.current {{cStep}}
      button(
        @click="goNext"
      )
        span NEXT
</template>

<script>
import HotStepper from './components/HotStepper'

export default {
  name: 'App',
  components: {
    HotStepper
  },

  data: function () {
    return {
      cStep: 0,
      steps: ['Fuck', 'Shit', 'Stack', 'Put it up on the wall', 'Check it out for a while']
    }
  },

  methods: {
    // Dummy methods for updating current step
    goNext: function () {
      this.cStep += 1
    },
    goBack: function () {
      this.cStep -= 1
    }
  }
}
</script>

<style lang="scss">
#app {
  font-family: 'Roboto', sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  width: 100vw;
  height: 100vh;
  color: #2c3e50;
  display: flex;
  align-items: center;
  align-content: center;
  justify-content: space-around;
  flex-direction: column;

  #debug {
    display: flex;
    flex-direction: row;
    align-items: center;
    align-content: stretch;
    justify-content: space-between;
    flex-wrap: wrap;
    max-width: 15rem;

    select {
      display: block;
      width: 100%;
      border: none;
      font-size: 1rem;
      margin-bottom: 1rem;

      option {
        font-size: 1rem;
        text-align: center;
      }
    }

    button {
      border-width: 0;
      outline: none;
      border-radius: 2px;
      box-shadow: 0 1px 4px rgba(0, 0, 0, .6);
      background-color: #2a68ae;
      color: #ecf0f1;
      transition: background-color .3s;

      &:hover {
        background-color: #1c3f70;
      }

      span {
        font-weight: 500;
        display: block;
        padding: 0.8rem 1.2rem;
      }
    }

    span.current {
      font-weight: 800;
    }
  }
}
</style>
