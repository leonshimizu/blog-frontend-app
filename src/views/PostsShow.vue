<template>
  <div class="show">
    <h1 id="showTitle">{{ message }}</h1>
    <hr>
    <div id="showCard" class="card text-dark bg-light mb-3">
    <div class="card-header">{{ post.id }}</div>
      <div class="card-body">
      <h5 class="card-title">{{ post.title }}</h5>
      <p class="card-text">{{ post.body }}</p>
      <p class="card-text"><img v-bind:src="post.image"></p>
      <p class="card-text">{{ post.created }}</p>
      <small>{{ post.user_id }} || {{ $parent.getUserId() }}</small>
      <div v-if="post.user_id == $parent.getUserId()">
        <p><button type="button" class="btn btn-outline-warning"><router-link v-bind:to="`${post.id}/edit`">Edit Post</router-link></button></p>
        <button type="button" class="btn btn-outline-danger" v-on:click="deleteFunction()">Delete Post</button>
      </div>
      </div>
    </div>
    <!-- <p><b>ID: </b>{{ post.id }}</p>
    <p><b>Title: </b>{{ post.title }}</p>
    <p><b>Body: </b>{{ post.body }}</p>
    <p><img v-bind:src="post.image"></p>
    <p><b>Created: </b>{{ post.created_at }}</p>
    <p><router-link v-bind:to="`${post.id}/edit`">Edit Post</router-link></p>
    <button v-on:click="deleteFunction()">Delete Post</button> -->
  </div>
</template>

<style>
  .show {
    text-align: center;
  }
  #showTitle {
    color: aliceblue;
  }
  #showCard {
    text-align: center;
  }
</style>

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
      },
      deleteFunction: function() {
        console.log("in the delete function");
        axios
          .delete(`/posts/${this.$route.params.id}`)
          .then(response => {
            console.log(response.data);
            this.$router.push("/posts");
          })
      }
    }
  };
</script>
