<template>
  <div class="index">
    <h1 id="welcome">{{ message }}</h1>
    <div class="card text-center">
    <div class="card-header">
      Featured
    </div>
    <div class="card-body" v-for="post in posts">
      <h5 class="card-title">{{ post.title | uppercase }}</h5>
      <p class="card-text"><img v-bind:src="post.image"></p>
      <a v-bind:href="`posts/${post.id}`" class="btn btn-primary">More Info</a>
      <hr>
    </div>
  </div>
  </div>
</template>

<style>
  #welcome {
    text-align: center;
    color: aliceblue;
  }
</style>

<script>
import Vue2Filters from 'vue2-filters'
import axios from 'axios';
  export default {
    mixins: [Vue2Filters.mixin],
    data: function () {
      return {
        message: "Welcome to the Blog!",
        posts: [],
        currentPost: {}
      };
    },
    created: function () {
      this.indexFunction();
    },
    methods: {
      indexFunction: function() {
        console.log("in the index function");
        axios
          .get('/posts')
          .then(response => {
            console.log(response.data);
            this.posts = response.data;
          })
      },
      // showModal: function(thePost) { // works but going to create a separate show page
      //   console.log("in the show modal");
      //   document.querySelector("#show-modal").showModal()
      //   this.currentPost = thePost;
      // }
    },
  };
</script>