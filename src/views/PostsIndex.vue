<template>
  <div class="posts-index">
    <h1>All Posts</h1>

    <div v-for="post in posts">
      <img v-bind:src="post.image" alt="">
      <h2><router-link v-bind:to="'/posts/' + post.id">{{ post.title }}</router-link></h2>
    </div>
  </div>
  </div>
</template>

<style>
</style>

<script>
var axios = require('axios');
export default {
  data: function() {
    return {
      posts: []
    };
  },
  created: function() {
    axios.get("/api/posts").then(response => {
      this.posts = response.data;
    });
  },
  methods: {}
};
</script>