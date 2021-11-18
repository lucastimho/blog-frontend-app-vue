<template>
  <div class="posts-show">
    <h3>{{ post.title }}</h3>
    <img :src="post.image" :alt="post.title" />
    <p>{{ post.body }}</p>
    <div>
      <router-link v-bind:to="`/posts/${post.id}/edit`">Edit this post</router-link>
      |
    </div>
    <router-link to="/posts">Back to all posts</router-link>
  </div>
</template>

<script>
import axios from "axios";
export default {
  data: function () {
    return {
      post: {},
    };
  },
  created: function () {
    axios.get("/posts/" + this.$route.params.id).then((response) => {
      this.post = response.data;
    });
  },
  methods: {},
};
</script>
