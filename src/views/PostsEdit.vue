<template>
  <div class="postsedit">
    <form v-on:submit.prevent="updatePost()">
      <h1>Create a Post</h1>
      <ul>
        <li v-for="error in errors" v-bind:key="error">{{ error }}</li>
      </ul>
      <div>
        <label>Title:</label>
        <textarea name="input" cols="30" rows="2" v-model="currentPostParams.title"></textarea>
      </div>
      <div>
        <label>Body:</label>
        <textarea name="input" cols="30" rows="6" v-model="currentPostParams.body"></textarea>
      </div>
      <div>
        <label>Image:</label>
        <textarea name="input" cols="30" rows="2" v-model="currentPostParams.image"></textarea>
      </div>
      <input type="submit" value="Submit" />
    </form>
    <button v-on:click="deletePost()">Delete</button>
  </div>
</template>

<script>
import axios from "axios";

export default {
  data: function () {
    return {
      currentPostParams: {},
      errors: [],
    };
  },
  created: function () {
    axios.get(`/posts/${this.$route.params.id}`).then((response) => {
      console.log("Post Info:", response.data);
      this.currentPostParams = response.data;
    });
  },
  methods: {
    updatePost: function () {
      axios
        .patch(`/posts/${this.$route.params.id}`, this.currentPostParams)
        .then((response) => {
          this.$router.push(`/posts/${response.data.id}`);
        })
        .catch((error) => console.log(error.response));
    },
    deletePost: function () {
      axios.delete(`/posts/${this.$route.params.id}`).then((response) => {
        console.log(response.data);
        this.$router.push("/posts");
      });
    },
  },
};
</script>
