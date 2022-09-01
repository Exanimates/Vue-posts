<template>
  <div class="panel">
    <h1 class="title">{{ post.title }}</h1>
    <div>{{ post.title }}</div>
    <div class="username">{{ post.username }}</div>
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
  .panel {
    position: relative;
    padding-bottom: 50px;

    background-color: white;
    height: 370px;
    margin: 10px;

    box-shadow: 10px 5px 5px #D3D3D3;

  }

  .title {
    color: #1E90FF;
  }

  .username {
    position: absolute;
    bottom: 0;
    color: #C0C0C0;
  }
</style>
