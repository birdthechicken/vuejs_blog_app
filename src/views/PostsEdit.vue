<template>
  <div class="posts-edit">
    <h1>Edit Post</h1>

   <ul>
     <li v-for="error in errors">
      {{ error }}
     </li>
   </ul>


   <form v-on:submit.prevent="submit()">
     <div>
       Title: <input v-model="post.title">
     </div>

     <div>
       Body: <input v-model="post.body">
     </div>

     <div>
       Image: <input v-model="post.image">
     </div>

     <input type="submit" value="Update Post">
    </form>
  </div>
</template>

<style>
</style>

<script>
var axios = require('axios');

export default {
  data: function() {
    return {
      errors: [],
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
  methods: {
    submit: function() {
     var params = {
                    title: this.post.title,
                    body: this.post.body,
                    image: this.post.image
                    }; 

      axios.patch("/api/posts/" + this.$route.params.id, params).then(response => {
        this.$router.push("/posts/" + this.$route.params.id);
      });
    }
  }
};
</script>