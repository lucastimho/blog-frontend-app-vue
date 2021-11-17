<template>
  <div class="postsnew">
    <img v-if="status" :src="`https://http.cat/${status}`" alt="" />
    <form v-on:submit.prevent="createPost()">
      <h1>Create a Post</h1>
      <ul>
        <li v-for="error in errors" v-bind:key="error">{{ error }}</li>
      </ul>
      <div>
        <label>Title:</label>
        <textarea name="input" cols="30" rows="2" v-model="newPostParams.title"></textarea>
        <small>{{ 100 - newPostParams.title.length }} characters remaining</small>
      </div>
      <div>
        <label>Body:</label>
        <textarea name="input" cols="30" rows="5" v-model="newPostParams.body"></textarea>
        <small>{{ 240 - newPostParams.body.length }} characters remaining</small>
      </div>
      <div>
        <label>Image:</label>
        <textarea name="input" cols="30" rows="2" v-model="newPostParams.image"></textarea>
        <small v-if="newPostParams.image.length === 0" class="text-danger">This post has no image</small>
      </div>
      <input type="submit" value="Submit" />
    </form>
  </div>
</template>

<script>
import axios from "axios";

export default {
  data: function () {
    return {
      newPostParams: { title: "", body: "", image: "" },
      errors: [],
      status: "",
    };
  },
  methods: {
    createPost: function () {
      axios
        .post("/posts", this.newPostParams)
        .then(() => {
          this.$router.push("/posts");
        })
        .catch((error) => {
          this.status = error.response.status;
          console.log(error.response);
        });
    },
  },
};
</script>
