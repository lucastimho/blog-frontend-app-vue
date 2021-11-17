<template>
  <div class="PostsIndex">
    <h1>List of All Posts</h1>
    <div
      v-for="post in posts"
      v-on:click="currentPost = post"
      v-bind:class="{ selected: post === currentPost }"
      :key="post.id"
    >
      <h3>{{ post.title }}</h3>
      <router-link v-bind:to="`/posts/${post.id}`">
        <img :src="post.image" :alt="post.title" />
      </router-link>
      <p>{{ post.body }}</p>
    </div>
  </div>
</template>

<style>
img {
  width: 250px;
}
.selected {
  color: white;
  background-color: lightskyblue;
  transition: background-color 1s ease;
}
</style>

<script>
import axios from "axios";
export default {
  data: function () {
    return {
      posts: [],
      currentPost: {},
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
