<template>
  <div class="hello">
    <h1>{{ post.title }}</h1>
    <div>{{ post.title }}</div>
    <div>{{ post.username }}</div>
  </div>
</template>

<script>
export default {
  name: 'PostComp',
  props: {
    post: Object
  }
}
</script>

<style scoped>
</style>
