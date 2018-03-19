<template lang="pug">
  div.hot-stepper
    ol
      li(
        v-for="(step, index) in steps"
      )
        div(
          :id="'htsr' + index",
          class="step-container"
        )
          div.icon
            span.number {{index + 1}}
          div.label
            span.text {{step}}
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
    $icon-cont-size: 1.8rem;

    ol {
      list-style: none;
      padding: 0;
      margin: 0;

      li {
        .step-container {
          display: flex;
          flex-direction: row;
          align-items: center;
          align-content: center;

          .icon {
            width: $icon-cont-size;
            height: $icon-cont-size;
            display: flex;
            align-items: center;
            align-content: center;
            flex-direction: row;
            justify-content: space-around;
            border-radius: 50%;

            .number {
            }
          }
          .label {
            .text {

            }
          }
        }
      }
    }
  }
</style>
