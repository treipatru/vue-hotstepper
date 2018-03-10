<template>
  <div class="hello">
    <ol>
      <li
        v-for="(step, index) in steps"
        :key="index"
        :id="'hs-cont' + index"
        :class="[
          {'pre': cStep < index},
          {'now': cStep === index},
          {'post': cStep > index}
        ]"
      >
        <div class="number">
          <span
            class="text"
          >
            {{index + 1}}
          </span>
          <span class="icon">
            <svg
              xmlns="http://www.w3.org/2000/svg"
              viewBox="0 0 512 512"><path d="M173.898 439.404l-166.4-166.4c-9.997-9.997-9.997-26.206 0-36.204l36.203-36.204c9.997-9.998 26.207-9.998 36.204 0L192 312.69 432.095 72.596c9.997-9.997 26.207-9.997 36.204 0l36.203 36.204c9.997 9.997 9.997 26.206 0 36.204l-294.4 294.401c-9.998 9.997-26.207 9.997-36.204-.001z"/></svg>
          </span>
          <div class="line"></div>
        </div>
        <div class="label" @click="updateStep(index)">
          <span>
            {{step}}
          </span>
        </div>
      </li>
    </ol>
    <div class="debug">
      <p>INDEX NOW: {{cStep}}</p>
      <select
        v-model="cStep"
      >
        <option
          v-for="(step,index) in steps"
          :key="index"
          :value="index"
        >
          {{step}}
        </option>
      </select>
      <button @click="goDown"> BACK </button>
      <button @click="goUp"> NEXT </button>
    </div>
  </div>
</template>


<script>
import anime from 'animejs'

export default {
  name: 'HotStepper',
  data() {
    return {
      cStep: 0,
      steps: ['Fuck', 'Shit', 'Stack', 'Fuck Shit Stack'],
      animations: {}
    }
  },
  methods: {
    updateStep: function (d) {
      if (d < this.cStep) {
        for (let i = d; i < this.steps.length; i++) {
          this.animations[i].seek(0)
        }
      } else if (d > this.cStep + 1) {
        for (let i = this.cStep; i < d; i++) {
          this.animations[i].restart()
        }
      } else if (d === this.cStep + 1) {
        this.animations[d-1].play()
      }
      this.cStep = d
      console.log(this.cStep)
    },
    goUp: function () {
      console.log(this.steps.maxLength)
      if (this.cStep !== this.steps.length) {
        this.cStep += 1
      }
    },
    goDown: function () {
      if (this.cStep !== 0) {
        this.cStep -= 1
      }
    }
  },
  mounted: function () {
    let vm = this

    for (let step in this.steps) {

      vm.animations[step] = anime.timeline({
        direction: 'forward',
        autoplay: false
      })

      vm.animations[step]
        .add({
          targets: '#hs-cont' + step + ' .text',
          duration: 300,
          opacity: [1, 0],
          easing: 'easeOutExpo'
        })
        .add({
          targets: '#hs-cont' + step + ' .icon',
          duration: 500,
          opacity: [0, 1],
          easing: 'easeOutExpo'
        })
    }
  }
}
</script>


<style lang="scss">
  $li-spacing: 1.5rem;
  $number-size: 2rem;
  $pre-background: #9e9e9e;
  $pre-color: #9e9e9e;
  $now-background: #5375ff;
  $now-color: #364ea9;
  $post-background: #d6d6d6;
  $post-color: #9e9e9e;

  .hello {
    ol {
      list-style: none;

      li {
        $parent: &;

        display: flex;
        flex-direction: row;
        margin-bottom: $li-spacing;

        .number {
          width: $number-size;
          height: $number-size;
          border-radius: 50%;
          position: relative;
          display: inline-block;
          border: 1px solid transparent;

          span {
            position: absolute;
            transform: translate(-50%, -50%);
            top: 50%;
            left: 50%;
          }

          .icon {

          }

          .text {

          }

          svg {
            width: 1.3rem;
            fill: #FFF;
          }
        }

        &.pre .number {
          border-color: $pre-color;

          .text {
            color: $pre-color;
          }
        }
        &.now .number {
          background: $now-background;

          .text {
            color: white;
          }
        }
        &.post .number {
          background: $post-background;

          .line {
            width: 1px;
            height: $number-size;
            background: $post-background;
            position: absolute;
            top: 100%;
            left: 50%;
          }

          .text {
            color: white;
          }
        }

        .label {
          display: flex;
          align-content: center;
          align-items: center;
          user-select: none;
          margin-left: 1rem;
        }

        &.pre .label {
          color:  $pre-color;
        }
        &.now .label {
          color:  $now-color;
          font-weight: 500;
        }
        &.post .label {
          color:  $post-color;
        }
      }
    }
  }
</style>
