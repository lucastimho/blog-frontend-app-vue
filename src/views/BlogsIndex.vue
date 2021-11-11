<template>
  <div class="BlogsIndex">
    <div v-for="post in posts" :key="post.id">
      <h3>{{ post.title }}</h3>
      <img v-vind:src="post.image" :alt="post.title" />
      <p>{{ post.body }}</p>
    </div>
  </div>
</template>

<style>
img {
  width: 250px;
}
</style>

<script>
import axios from "axios";
export default {
  data: function () {
    return {
      posts: [],
    };
  },
  created: function () {
    this.indexPosts();
  },
  methods: {
    indexPosts: function () {
      axios.get("/posts").then((response) => {
        this.posts = response.data;
        console.log("All posts", this.posts);
      });
    },
  },
};
</script>
