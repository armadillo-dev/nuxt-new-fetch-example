<template>
  <v-layout
    column
  >
    <v-flex
      xs12
      sm8
      md6
    >
      <v-btn to="/">Back to List</v-btn>
      <template v-if="$fetchState.pending">
        <p>fetching...</p>
      </template>
      <template v-else>
        <h4>{{ post.title }}</h4>
        <p>{{ post.body }}</p>
      </template>
    </v-flex>
  </v-layout>
</template>

<script>
export default {
  name: 'DetailPage',
  data() {
    return {
      post: {},
    }
  },
  activated() {
    console.log('kkw executed activated hook')
    if (this.$fetchState.timestamp <= (Date.now() - 30000)) {
      console.log('kww call fetch in activated hook')
      this.$fetch()
    }
  },
  async fetch() {
    const response = await fetch(`https://jsonplaceholder.typicode.com/posts/${this.$route.params.id}`)
    this.post = await response.json()
  },
}
</script>
