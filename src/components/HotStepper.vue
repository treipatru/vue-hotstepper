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
          div.icon(
            :id="'htsr' + index + 'icon'"
          )
            span.number(
              :id="'htsr' + index + 'number'"
            ) {{index + 1}}
            span.check(
              :id="'htsr' + index + 'check'"
            )
              svg(
                xmlns="http://www.w3.org/2000/svg",
                viewBox="0 0 512 512"
              )
                path(
                  d="M173.898 439.404l-166.4-166.4c-9.997-9.997-9.997-26.206 0-36.204l36.203-36.204c9.997-9.998 26.207-9.998 36.204 0L192 312.69 432.095 72.596c9.997-9.997 26.207-9.997 36.204 0l36.203 36.204c9.997 9.997 9.997 26.206 0 36.204l-294.4 294.401c-9.998 9.997-26.207 9.997-36.204-.001z",
                  stroke-width="1"
                  class="check-line"
                )
          div.label
            span.text {{step}}
</template>


<script>
import * as pop from 'popmotion'

export default {
  name: 'HotStepper',
  computed: {
    state: function () {
      let c = this.cStep

      return this.steps.map((el, i) => {
        if (i < c) {
          return 'post'
        } else if (i === c) {
          return 'now'
        } else {
          return 'pre'
        }
      })
    },
    circles: function () {
      let a = Array.from(document.querySelectorAll('.step-container .icon'))
      return a.map(el => pop.styler(el))
    },
    numbers: function () {
      let a = Array.from(document.querySelectorAll('.step-container .number'))
      return a.map(el => pop.styler(el))
    },
    checks: function () {
      let a = Array.from(document.querySelectorAll('.step-container .check'))
      return a.map(el => pop.styler(el))
    }
  },
  data() {
    return {
      anims: {
      }
    }
  },

  methods: {
    getCssProperty: function (id, property) {
      let el = document.getElementById(id)
      return window.getComputedStyle(el).getPropertyValue(property)
    }
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
    cStep: function (nVal, oVal) {
      let vm = this

      //Warn if cStep is invalid
      if (nVal < 0 || nVal > vm.steps.length - 1) {
        console.log('Current step (' + nVal + ') out of bounds')
      }
    },

    // Check for changed elements and dispatch animations
    state: function (nVal, oVal) {
      let vm = this
      let a = nVal.map( (el, i) => {

        if (el !== oVal[i]) {
          const curColor = vm.getCssProperty('htsr' + i + 'icon', 'background-color')

          if (el === 'post') {
            pop.keyframes({
              values: [curColor , '#989898'],
              duration: 200
            }).start(vm.circles[i].set('backgroundColor'))

          }

          if (el === 'now') {
            pop.keyframes({
              values: [curColor , '#14D790'],
              duration: 200
            }).start(vm.circles[i].set('backgroundColor'))
          }

          if (el === 'pre') {
            pop.keyframes({
              values: [curColor , 'rgba(0, 0, 0, 0)'],
              duration: 200
            }).start(vm.circles[i].set('backgroundColor'))
          }
        }

      })

        return a
    }
  }
}
</script>


<style lang="scss">
  .hot-stepper {
    $icon-cont-size: 2rem;

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
          margin-bottom: 1.5rem;

          .icon {
            width: $icon-cont-size;
            height: $icon-cont-size;
            position: relative;
            border-radius: 50%;

            .number, .check {
              position: absolute;
              top: 50%; right: 50%;
              transform: translate(50%,-50%);
            }

            .number {
            }

            .check {
              opacity: 0;

              svg {
                width: 1rem;
                fill: #FFF;
              }
            }

          }
          .label {
            margin-left: 1rem;

            .text {
            }
          }
        }
      }
    }
  }
</style>
