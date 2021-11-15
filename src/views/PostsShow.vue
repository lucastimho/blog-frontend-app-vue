<template>
  <div class="posts-show">
    <h3>{{ post.title }}</h3>
    <img v-vind:src="post.image" :alt="post.title" />
    <p>{{ post.body }}</p>
    <router-link to="/">Back to all posts</router-link>
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
