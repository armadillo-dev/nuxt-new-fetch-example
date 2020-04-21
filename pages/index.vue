<template>
  <v-layout
    column
    justify-center
    align-center
  >
    <v-flex
      xs12
      sm8
      md6
    >
      <v-data-table
        :headers="headers"
        :items="posts"
        @click:row="onClick"
      />
    </v-flex>
  </v-layout>
</template>

<script>
export default {
  name: 'ListPage',
  data() {
    return {
      headers: [
        { text: 'id', value: 'id' },
        { text: 'title', value: 'title' },
      ],
      posts: [],
    }
  },
  async fetch() {
    const response = await fetch('https://jsonplaceholder.typicode.com/posts')
    this.posts = await response.json()
  },
  methods: {
    onClick({ id }) {
      this.$router.push(`/${id}`)
    },
  }
}
</script>
