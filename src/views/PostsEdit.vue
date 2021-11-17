<template>
  <div class="update">
    <br>
    <form v-on:submit.prevent="submit()">
      <h1 id="editPost">{{ message }}</h1>
      <ul>
        <li v-for="error in errors" v-bind:key="error">{{ error }}</li>
      </ul>
      <div class="card">
        <ul class="list-group list-group-flush">
          <li class="list-group-item"><label>Title:</label>
          <input type="text" v-model="editPostParams.title" /></li>
          <li class="list-group-item"><label>Body:</label>
          <input type="text" v-model="editPostParams.body" /></li>
          <li class="list-group-item"><label>Image:</label>
          <input type="text" v-model="editPostParams.image" /></li>
        </ul>
        <input type="submit" value="Submit" />
      </div>
    </form>
    <!-- <form v-on:submit.prevent="submit()">
      <h1>Edit Blog</h1>
      <ul>
        <li v-for="error in errors" v-bind:key="error">{{ error }}</li>
      </ul>
      <div>
        <label>Title:</label>
        <input type="text" v-model="editPostParams.title" />
      </div>
      <div>
        <label>Body:</label>
        <input type="text" v-model="editPostParams.body" />
      </div>
      <div>
        <label>Image:</label>
        <input type="text" v-model="editPostParams.image" />
      </div>
      <input type="submit" value="Submit" />
    </form> -->
  </div>
</template>

<style>
  #editPost {
    color: aliceblue;
    text-align: center;
  }
</style>

<script>
  import axios from "axios";

  export default {
    data: function () {
      return {
        editPostParams: {},
        errors: [],
        message: "Edit Post:"
      };
    },
    methods: {
      submit: function () {
        axios
          .patch("/posts/" + this.$route.params.id, this.editPostParams)
          .then((response) => {
            console.log(response.data);
            this.$router.push("/posts");
          })
          .catch((error) => {
            this.errors = error.response.data.errors;
          });
      },
      showFunction: function() {
        console.log("in the show function");
        axios 
          .get(`/posts/${this.$route.params.id}`)
          .then(response => {
            console.log(response.data);
            this.editPostParams = response.data;
          })
      }
    },
    created: function() {
      this.showFunction();
    }
  };
</script>