<template>
  <div>
    <h1>Canvas test</h1>
    <div class="canvas-container">
      <Radian class="canvas-content" />
      <Vector class="canvas-content" />
    </div>
  </div>
</template>

<script>
export default {
  head() {
    return {
      title: 'canvas page'
    }
  }
}
</script>

<style lang="scss">
.canvas-container {
  width: 100%;
  /*   display: flex; */
  .canvas-content {
    /*     width: 50%; */
  }
}
</style>
