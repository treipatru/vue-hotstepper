<template>
  <div id="app">
    <hot-stepper/>
  </div>
</template>

<script>
import HotStepper from './components/HotStepper'

export default {
  name: 'App',
  components: {
    HotStepper
  }
}
</script>

<style>
#app {
  font-family: 'Roboto', sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  margin-top: 60px;
  display: flex;
  align-items: center;
  align-content: center;
  flex-direction: column;
}
</style>
