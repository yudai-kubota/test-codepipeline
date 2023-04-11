<template>
  <div class="calc-container">
    <h5>配列{{ vectorName }}</h5>
    <table>
      <thead>
        <tr>
          <td>put [X, Y]: [</td>
          <td><input type="text" size="3" v-model="vector[0]"></td>
          <td>, </td>
          <td><input type="text" size="3" v-model="vector[1]"> ]</td>
        </tr>
      </thead>
    </table>

    <p>vector length: {{ vectorLength }}</p>
    <p>unit vector: {{ unitVector }}</p>
  </div>
</template>

<script>
export default {
  props: [
    'vectorName'
  ],
  data() {
    return {
      vector: [3, 5],
      vectorLength: 0,
      unitVector: [0, 0]
    }
  },
  watch: {
    vector: {
      handler(newVal, oldVal) {
        this.createUnitVector()
      },
      deep: true
    }
  },
  methods: {
    createUnitVector() {
      this.vectorLength = Math.sqrt(this.vector[0] * this.vector[0] + this.vector[1] * this.vector[1])
      this.unitVector = [this.vector[0] / this.vectorLength, this.vector[1] / this.vectorLength]
      this.$emit('did-calc-vector', this.vector, this.vectorLength, this.unitVector)
    }
  },
  mounted() {
    this.createUnitVector()
  }
}
</script>

<style lang="scss">
.calc-container {
  width: 50%;
}
</style>
