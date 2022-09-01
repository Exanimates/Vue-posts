<template>
  <div class="content">
    <div class="search">
      <b-form-input class="input" type="text" v-model="searchText" placeholder="Filter by author"/>
    </div>
    <div class="post-container">
      <PostComp v-for="post in filteredPosts" :key="post.id" :post="post"/>
    </div>
  </div>
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
  .input {
    width: 300px;
    margin: auto;    
  }
  .content {
    background-color: aliceblue;
  }
  .search {
    text-align: center;
  }

  .post-container {
    display: grid;
    align-items: center;
    justify-content: center;
    border-top: 2px solid white;
    margin-top: 20px;
    height: 60%;
    grid-template-columns: repeat(auto-fit, 300px);
  }
</style>
