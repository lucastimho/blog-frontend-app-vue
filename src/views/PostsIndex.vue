<template>
  <div class="PostsIndex">
    <div>
      Search by Title:
      <input type="text" v-model="titleFilter" list="titles" />
      <datalist id="titles">
        <option v-for="post in posts" :key="post.id">{{ post.title }}</option>
      </datalist>
    </div>
    <div>
      <button v-on:click="setSortAttribute('title')">Sort by Title</button>
      <button v-on:click="setSortAttribute('body')">Sort by Body Text</button>
    </div>
    <h1>List of All Posts</h1>
    <div>
      <div class="row">
        <div class="col-sm-6">
          <div
            class="card"
            v-for="post in orderBy(filterBy(posts, titleFilter, 'title', 'body'), sortAttribute)"
            :key="post.id"
          >
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
import Vue2Filters from "vue2-filters";
export default {
  mixins: [Vue2Filters.mixin],
  data: function () {
    return {
      posts: [],
      currentPost: {},
      titleFilter: "",
      sortAttribute: "",
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
    setSortAttribute: function (inputAttribute) {
      this.sortAttribute = inputAttribute;
    },
  },
};
</script>
