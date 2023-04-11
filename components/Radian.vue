<template>
  <div class="radian-container">
    <h3>Radian CheatSheet</h3>
    <table>
      <thead>
        <tr>
          <td><p>put degrees:</p></td>
          <td><input type="text" size="3" v-model="degrees"></td>
        </tr>
      </thead>
    </table>
    <p>digress: {{ degrees }}</p>

    <p>radius: {{ radius }}</p>
    <p>sin: {{ sin }}</p>
    <p>cos: {{ cos }}</p>

    <table>
      <thead>
        <tr>
          <td><p>put distance:</p></td>
          <td><input type="text" size="3" v-model="distance"></td>
        </tr>
      </thead>
    </table>

    <p>distance(vectorLength): {{ distance }}</p>
    <p>角度digress,距離distance 移動後の座標: {{ place }}</p>

    <p>↓graff: distance, radius<br>
      高さ(sin * distance):{{ sin * distance }},<br>
      底辺(cos * distance):{{ cos * distance }}
    </p>
    <div class="line-box">
      <div class="base-line base-x">x</div>
      <div class="base-line base-y">&nbsp;y</div>
      <div class="line-content-row" :style="lineStyle">
        <div class="line-content none" />
        <div class="line-content" />
      </div>
      <div class="line-content-trajectory anime" :style="trajectoryStyle" ref="trajectory" />
    </div>

  </div>
</template>

<script>
export default {
  data() {
    return {
      degrees: 30,
      radius: 0,
      sin: 0,
      cos: 0,
      distance: 400,
      place: [],
    }
  },
  computed: {
    lineStyle() {
      return {
        transform: 'rotate(-' + this.radius + 'rad)',
        width: this.distance + 'px'
      }
    },
    trajectoryStyle() {
      if (this.$refs.trajectory) {
        this.$refs.trajectory.classList.remove('anime')
        this.$refs.trajectory.style.opacity = 0
        setTimeout(() => {
          this.$refs.trajectory.classList.add('anime')
        }, 200)
      }
      return {
        width: this.distance + 'px',
        height: this.distance + 'px',
        position: 'absolute',
        zIndex: '-1',
        borderRadius: '50%',
        transform: 'rotate(90deg) scale(-1, 1)',
        transition: 'all 1.5s',
        background: 'conic-gradient(red ' + this.degrees + 'deg, #FFFFFF00 ' + this.degrees + 'deg'
      }
    }
  },
  watch: {
    degrees(newVal, oldVal) {
      this.createSinCos()
      this.calcPlace()
    },
    distance(newVal, oldVal) {
      this.createSinCos()
      this.calcPlace()
    }
  },
  methods: {
    degToRad(degrees) {
      this.radius = degrees * Math.PI / 180
    },
    createSinCos() {
      this.degToRad(this.degrees)

      this.sin = Math.sin(this.radius)
      this.cos = Math.cos(this.radius)
    },
    calcPlace() {
      let A = [0.0, 0.0]

      this.place = [
        A[0] + this.cos * this.distance,
        A[1] + this.sin * this.distance
      ]
    }
  },
  mounted() {
    this.createSinCos()
    this.calcPlace()
  }
}
</script>

<style lang="scss">
.radian-container {
  border: 1px solid black;

  .line-box {
    width: 400px;
    height: 400px;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    background-color: #00000020;
    position: relative;

    &.radias {
      height: 200px;
    }

    .line-content-row {
      width: 100%;
      height: 2px;
      display: flex;
      z-index: 0;
      transition: all 1s;

      .line-content {
        width: 50%;
        height: 100%;
        background-color: red;
        background: conic-gradient(red 6deg);
        &.none {
          background-color: unset;
        }
      }
    }
    .base-line {
      width: 100%;
      height: 2px;
      background-color: black;
      position: absolute;
      z-index: 10;
      &.base-y {
        width: 2px;
        height: 100%;
        left: 50%;
      }
    }
    .anime {
      animation: backgroundAnimation 3s infinite;
      animation-direction: alternate;
      @keyframes backgroundAnimation {
        from {
          opacity: 0;
        }
        to {
          opacity: 1.0;
        }
      }
    }
  }
}
</style>
