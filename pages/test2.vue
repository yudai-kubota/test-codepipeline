<template>
  <h1>TEST2</h1>
</template>

<script>
import Axios from 'axios'
export default {

  methods: {
    async testA() {
      await Axios.get('https://jsonplaceholder.typicode.com/photos')
                 .then(function (response) {
                   console.log("A",response);
                 })
    },
    async testB() {
      await Axios.get('https://jsonplaceholder.typicode.com/users')
                 .then(function (response) {
                   console.log("B",response);
                 })
    },
    async testD() {
      await new Promise(resolve => setTimeout(resolve, 3000))
    },
    /* testA() {
     *   Axios.get('https://qiita.com/api/v2/items?page=1&per_page=100')
     *        .then(function (response) {
     *          console.log("A",response);
     *        })
     * },
     * testB() {
     *   Axios.get('https://qiita.com/api/v2/items?page=2&per_page=20')
     *        .then(function (response) {
     *          console.log("B",response);
     *        })
     * }, */
    async testC() {
      console.log("C")
    },
  },
  async mounted() {
    await this.testD()
    await this.testA()
    await this.testB()
    await this.testC()
  }
}
</script>
