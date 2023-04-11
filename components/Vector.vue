<template>
  <div class="vector-container">
    <h3>Vector CheatSheet</h3>
    <div class="calc-row">
      <VectorCalc :vectorName='nameA' @did-calc-vector="didCalcVector" />
      <VectorCalc :vectorName='nameB' @did-calc-vector="didCalcVector" />
    </div>

  </div>
</template>

<script>
export default {
  data() {
    return {
      nameA: 'A',
      nameB: 'B'
    }
  },
  watch: {
  },
  methods: {
    didCalcVector(vector, vectorLength, unitVector) {
      console.log(vector)
      console.log(vectorLength)
      console.log(unitVector)
    }
  },
  mounted() {
  }
}
</script>

<style lang="scss">
.vector-container {
  width: 100%;
  border: 1px solid black;
  border-left: none;

  .calc-row {
    width: 100%;
    display: flex;
  }
}
</style>
