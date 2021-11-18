<template>
  <div class="PostsIndex">
    <h1>List of All Posts</h1>
    <div class="row">
      <div class="col-sm-6">
        <div class="card" v-for="post in posts" :key="post.id">
          <span>
            <div class="card-body">
              <h5 class="card-title">{{ post.title }}</h5>
              <img :src="post.image" alt="post.title" />
              <p class="card-text">{{ post.body }}</p>
              <p class="card-text">Created: {{ relativeDate(post.created_at) }}</p>
              <p class="card-text">Updated: {{ relativeDate(post.updated_at) }}</p>
              <router-link v-bind:to="`/posts/${post.id}`" class="btn btn-primary">Read More</router-link>
            </div>
          </span>
        </div>
      </div>
    </div>
    <!-- <div
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
    </div> -->
  </div>
</template>

<style>
img {
  width: 250px;
}
/* .selected {
  color: white;
  background-color: lightskyblue;
  transition: background-color 1s ease;
} */
span:hover {
  color: white;
  background-color: lightskyblue;
  transition: background-color 1s ease;
}
</style>

<script>
import axios from "axios";
import moment from "moment";
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
    relativeDate: function (date) {
      return moment(date).fromNow();
    },
  },
};
</script>
