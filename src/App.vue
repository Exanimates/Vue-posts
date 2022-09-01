<template>
  <input type="text" @input="event => searchText = event.target.value"/>
  <PostComp v-for="post in filteredPosts" :key="post.id" :post="post"/>
</template>

<script>
import PostComp from './components/PostComp.vue';

export default {
  name: 'App',
  components: {
    PostComp
  },

  data() {
    return {
      users: [],
      posts: [],
      searchText: ''
    }
  },

  computed: {
    filteredPosts: function () {
      if (this.searchText) return this.posts.filter(post => post.username.startsWith(this.searchText))

      return this.posts;
    }
  },

  methods: {
    postUsersMap() {
      this.posts = this.posts.map((post)=>{
          let userById = this.users.find(user=> user.id === post.userId)
          if(userById.name) {
            post.username = userById.name;
          }
          return post;
      })
    }
  },

  async created() {
    this.posts = await (await fetch("https://jsonplaceholder.typicode.com/posts")).json();
    this.users = await (await fetch("https://jsonplaceholder.typicode.com/users")).json();
    this.postUsersMap();
  }


}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
