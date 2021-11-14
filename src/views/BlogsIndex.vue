<template>
  <div class="home">
    <h1>{{ message }}</h1>
    <ul>
      <li v-for="post in posts">
        <p>ID: {{ post.id }}</p>
        <p>Title: {{ post.title }}</p>
        <p><img v-bind:src="post.image"></p>
        <button v-on:click="showModal(post)">Show More Info</button>
      </li>
    </ul>
    <dialog id="show-modal">
      <form method="dialog">
        <p><b>Title:</b> {{ currentPost.title }}</p>
        <p><b>Body:</b> {{ currentPost.body }}</p>
        <p><b>Created:</b> {{ currentPost.created_at }}</p>
        <button>Close</button>
      </form>
    </dialog>
  </div>
</template>

<style></style>

<script>
import axios from 'axios';
  export default {
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
      showModal: function(thePost) {
        console.log("in the show modal");
        document.querySelector("#show-modal").showModal()
        this.currentPost = thePost;
      }
    },
  };
</script>