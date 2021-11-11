<template>
  <div class="home">
    <h1>{{ message }}</h1>
    <div v-for="post in posts" :key="post.id">
      <h2>{{ post }}</h2>
    </div>
  </div>
</template>

<style></style>

<script>
import axios from "axios";
export default {
  data: function () {
    return {
      message: "Welcome to Vue.js!",
      posts: [],
    };
  },
  created: function () {
    this.indexPosts();
  },
  methods: {
    indexPosts: function () {
      axios.get("http://localhost:3000/posts").then((response) => {
        this.posts = response.data;
        console.log("All posts", this.posts);
      });
    },
  },
};
</script>
