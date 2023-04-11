<template>
  <div>
    <h1 v-if="!user">
      不正なユーザ
    </h1>
    <h1 v-if="user">
      ユーザID: {{ user.name }}
    </h1>
  </div>
</template>

<script>
export default {
  data() {
    return {
      id: this.$route.params.id,
      users: [
        {
          id: 1, name: 'John Doe'
        },
        {
          id: 2, name: 'Kevin Smith'
        },
        {
          id: 3, name: 'Harry Bosch'
        }
      ]
    }
  },
  computed: {
    user() {
      return this.users.find(user => user.id == this.id)
    }
  },
  created() {
    console.log(this.$route)
  },
  mounted() {
    console.log(this.$route)
  }
}
</script>
