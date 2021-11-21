<template>
  <div class="index">
    <h1 id="welcome">{{ message }}</h1>
    <button v-on:click="flipSortOrder()">Flip Sort Order</button>
    <p>Search: <input type="text" v-model="searchTerm" list="titles"></p>
    <datalist id="titles">
      <option v-for="post in posts">{{ post.title }}</option>
    </datalist>
    <div class="card text-center">
    <div class="card-header">
      Featured
    </div>
    <div class="card-body" v-for="post in orderBy(filterBy(posts, searchTerm, 'title'), 'title', sortOrder)">
      <h5 class="card-title">{{ post.title }}</h5>
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
        currentPost: {},
        searchTerm: "",
        sortOrder: 1
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
      flipSortOrder: function() {
        this.sortOrder = this.sortOrder * -1
      }
      // showModal: function(thePost) { // works but going to create a separate show page
      //   console.log("in the show modal");
      //   document.querySelector("#show-modal").showModal()
      //   this.currentPost = thePost;
      // }
    },
  };
</script>