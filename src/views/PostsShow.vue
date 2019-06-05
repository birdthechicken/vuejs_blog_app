<template>
  <div class="posts-show">
    <h2>{{ post.title }}</h2>

    <p>{{ post.body }}</p>
    
    <router-link class="btn btn-warning m-1" v-bind:to="'/posts/' + post.id + '/edit'">Edit</router-link>

    <img v-bind:src="post.image">


  </div>
</template>

<style>
</style>

<script>
var axios = require('axios');

export default {
  data: function() {
    return {
      post: {
                title: "",
                body: "",
                image: ""  
              }
    };
  },
  created: function() {
    axios.get("/api/posts/" + this.$route.params.id ).then(response => {
      this.post = response.data;
    });
  },
  methods: {}
};
</script>