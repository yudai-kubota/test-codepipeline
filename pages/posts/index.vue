<template>
  <div>
    <h1>記事一覧</h1>
    <ul>
      <li v-for="post in posts" :key="post.id">
        {{ post.title }}
      </li>
    </ul>
  </div>
</template>

<script>
import Axios from 'axios'

export default {
  head() {
    return {
      title: 'posts page'
    }
  },
  layout: 'common',

  async asyncData({ $axios }) {
    const posts = await $axios.$get(
      "https://jsonplaceholder.typicode.com/posts/"
    );
    return { posts };
  },
  data() {
    /* return {
     *   posts: ""
     * } */
  },
  methods: {
    async test() {
      Axios.get('https://jsonplaceholder.typicode.com/posts').then(response => {
        this.posts = response.data
      })
    },
  },
  mounted() {
    /*     this.test() */
  }
}
</script>
