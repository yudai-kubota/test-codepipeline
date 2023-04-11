<template>
  <div class="usagi-container">
    <div class="usagi-control-row">
      <div class="control-button" @click="controlChange('background')">
        usagi is background
      </div>
      <div class="control-button" @click="controlChange('rotated')">
        usagi is rotated
      </div>
      <div class="control-button" @click="pointerChange()">
        pointer is exist
      </div>
    </div>
    <div class="usagi-content-row">
      <div class="usagi-content" :style="imgStyle" v-if="mode === 'background'" />
      <div class="usagi-content r" v-for="n, i in count" :key="i" v-bind:style="imgCountStyle" v-if="mode === 'rotated'" ref="tests" />

      <div class="pointer" ref="pointer" />
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      w: 0,
      h: 0,
      count: 100,
      mode: 'background',
      pointer: false
    }
  },
  computed: {
    imgCountStyle() {
      let width   = this.w / this.count * 10
      return {
        width: width + 'px',
        height: width + 'px',
        backgroundRepeat: 'no-repeat',
        backgroundSize: 'contain'
      }
    },
    imgStyle() {
      let size = this.w / 10
      return {
        width: '100%',
        height: '100%',
        backgroundSize: size + 'px',
        backgroundRepeat: 'repeat'
      }
    }
  },
  methods: {
    resized() {
      this.w = window.innerWidth
      this.h = window.innerHeight
    },
    countTest(n) {
      console.log(n)
    },
    controlChange(mode) {
      this.mode = mode
    },
    pointerChange() {
      this.pointer = !this.pointer

      /*  */
      let rect = 0
      this.$refs.tests.forEach(test => {
        rect = test.getBoundingClientRect()
        console.log(rect)
      })
      /*  */


      if (this.pointer) {
        let randomElm = this.$refs.pointer
        let randomTop = 50
        let randomLeft = 50

        randomElm.style.top = randomTop + "%"
        randomElm.style.left = randomLeft + "%"

        let timer = setInterval(() => {
          if (Math.random() * 2 < 1) {
            randomTop++
          } else {
            randomTop--
          }

          if (Math.random() * 2 < 1) {
            randomLeft++
          } else {
            randomLeft--
          }

          randomElm.style.left = randomLeft + "%"
          randomElm.style.top = randomTop + "%"
        }, 100)
      }
    }
  },
  mounted() {
    window.addEventListener('resize', this.resized)
    setTimeout(() => {
      this.resized()
    }, 200)
  },
  beforeDestroy() {
    window.removeEventListener('resize', this.resized)
  }
}
</script>

<style lang="scss">
.usagi-container {
  width: 100%;
  height: 100vh;
  display: flex;

  .usagi-control-row {
    width: 100%;
    height: 20vh;
    display: flex;
    flex-wrap: wrap;
    justify-content: center;
    .control-button {
      width: 30%;
      height: 20px;
      text-align: center;
      line-height: 20px;
      cursor: pointer;
    }
  }

  .usagi-content-row {
    width: 100%;
    height: 80vh;
    display: flex;
    flex-wrap: wrap;
    overflow: hidden;
    position: absolute;
    top: 20vh;
    left: 0;

    .usagi-content {
      background: url("~@/assets/suraud_square.gif");
      transition: all 2s;
    }
    .r:hover {
      transition: .5s;
      transform: rotate( 360deg );
    }
    .pointer {
      width: 10px;
      height: 10px;
      background-color: red;
      border-radius: 50%;
      position: absolute;
      transition: .1s;
      transform: translate(-50%, -50%);
    }
  }
}
</style>
