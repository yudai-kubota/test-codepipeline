<template>
  <div class="footer">
    <nuxt-link to="/">Home</nuxt-link>
    <nuxt-link to="/test">Test</nuxt-link>
    <nuxt-link to="/test2">Test2</nuxt-link>
    <nuxt-link to="/test3">Test3</nuxt-link>
    <nuxt-link to="/posts">Posts</nuxt-link>
    <nuxt-link to="/users">user-index</nuxt-link>
    <nuxt-link :to="{ name: 'users-list' }">user-list</nuxt-link>
    <nuxt-link to="/usagi"">usagi</nuxt-link>
    <nuxt-link to="/canvas"">canvas</nuxt-link>
  </div>
</template>

<style lang="scss">
.footer {
  width: 100%;
  display: flex;
  flex-wrap: wrap;
  a {
    width: 50%;
  }
}
</style>
