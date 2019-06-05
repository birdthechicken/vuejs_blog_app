<template>
  <div class="posts-new">
   <h1>New Post</h1>

   <ul>
     <li v-for="error in errors">
      {{ error }}
     </li>
   </ul>


   <form v-on:submit.prevent="submit()">
     <div>
       Title: <input v-model="newPostTitle">
     </div>

     <div>
       Body: <input v-model="newPostBody">
     </div>

    
     <div>
       Image: <input v-model="newPostImage">
     </div>

     <input type="submit" value="Create Post">
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
      newPostTitle: "",
      newPostBody: "",
      newPostImage: "",
      errors: []
    };
  },
  created: function() {},
  methods: {
    submit: function () {
      console.log("Create the post...");

      var params = {
                    title: this.newPostTitle,
                    body: this.newPostBody,
                    image: this.newPostImage
                    };

      axios.post("/api/posts", params).then(response => {
       this.$router.push("/");
      }).catch(error => {
        this.errors = error.response.data.errors;
      });
    }
  }
};
</script>