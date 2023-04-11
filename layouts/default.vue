<template>
  <div>
    <!-- <img src="~/assets/suraud.gif"> -->
    <Nuxt />
    <Footer />
  </div>
</template>

<script>
export default {
  head: {
    bodyAttrs: {
      class: 'body-class'
    }
  }
}
</script>

<style lang="scss">
.body-class {
  margin: 0;
}
</style>
