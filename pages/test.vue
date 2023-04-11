<template>
  <div class="test-container">
    <div class="left-content" />
    <div class="right-content" />
  </div>
</template>

<script>
export default {
  head() {
    return {
      title: 'test page'
    }
  },
  layout: 'common',
  methods: {
    async testA() {
      const A = await this.testB(10)
      const B = await this.testB(20)
      const C = await this.testB(30)
      return A + B - C
    },
    testB(v) {
      return v
    },
    testFu() {
      this.testA().then((v) => {
        console.log(v)
      })
    },
  },
  mounted() {
    this.testFu()
  }
}
</script>

<style lang="scss">
.test-container {
  width: 100%;
  display: flex;

  .left-content {
    width: 50%;
    height: 400px;
    background-color: red;
    position: sticky;
    top: 0;
  }
  .right-content {
    width: 50%;
    height: 2000px;
    background-color: blue;
  }
}
</style>
