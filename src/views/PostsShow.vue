<template>
  <div class="home">
    <h1>{{ message }}</h1>
    <hr>
    <p><b>ID: </b>{{ post.id }}</p>
    <p><b>Title: </b>{{ post.title }}</p>
    <p><b>Body: </b>{{ post.body }}</p>
    <p><img v-bind:src="post.image"></p>
    <p><b>Created: </b>{{ post.created_at }}</p>
  </div>
</template>

<style></style>

<script>
import axios from 'axios'
  export default {
    data: function () {
      return {
        message: "Welcome to the Show!",
        post: {}
      };
    },
    created: function () {
      this.showFunction()
    },
    methods: {
      showFunction: function() {
        console.log("in the show function");
        // console.log(this.$route.params.id) // gets whatever the params are in the url
        axios 
          .get(`/posts/${this.$route.params.id}`)
          .then(response => {
            console.log(response.data);
            this.post = response.data;
          })
      }
    },
  };
</script>
