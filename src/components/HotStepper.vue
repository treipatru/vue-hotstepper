<template lang="pug">
  div.hot-stepper
    ol
      li(
        v-for="(step, index) in steps"
      ) {{step}}
</template>


<script>

export default {
  name: 'HotStepper',
  data() {
    return {
    }
  },

  methods: {
  },

  mounted: function () {
  },

  props: {
    steps: {
      type: Array,
      required: true
    },
    cStep: {
      type: Number,
      required: true
    }
  },

  watch: {
  }
}
</script>


<style lang="scss">
  .hot-stepper {
    ol {
      list-style: none;
      padding: 0;
      margin: 0;
    }
  }
</style>
