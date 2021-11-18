<template>
  <div id="app">
    <div class="alert alert-success alert-dismissible fade show" role="alert" v-if="isLoggedIn()">
      <strong>Successfully Logged In!</strong>
      You are free to make posts now.
      <button type="button" class="btn-close" data-bs-dismiss="alert" aria-label="Close"></button>
    </div>
    <!-- <div id="nav">
      <router-link to="/">Home</router-link>
      |
      <router-link to="/posts">All Posts</router-link>
      |
      <router-link to="/posts/new">Create a Post</router-link>
      |
      <router-link to="/about">About</router-link>
      |
      <router-link to="/test">Test</router-link>
      |
      <router-link to="/signup">Sign Up</router-link>
      |
      <router-link to="/login">Login</router-link>
      |
      <router-link to="/logout">Logout</router-link>
    </div> -->
    <nav class="navbar navbar-expand-lg navbar-light bg-light">
      <div class="container-fluid">
        <a class="navbar-brand" href="/">Home</a>
        <button
          class="navbar-toggler"
          type="button"
          data-bs-toggle="collapse"
          data-bs-target="#navbarSupportedContent"
          aria-controls="navbarSupportedContent"
          aria-expanded="false"
          aria-label="Toggle navigation"
        >
          <span class="navbar-toggler-icon"></span>
        </button>
        <div class="collapse navbar-collapse" id="navbarSupportedContent">
          <ul class="navbar-nav me-auto mb-2 mb-lg-0">
            <li class="nav-item">
              <a class="nav-link active" aria-current="page" href="/posts">All Posts</a>
            </li>
            <li class="nav-item" v-if="!isLoggedIn()">
              <a class="nav-link" href="/login">Login</a>
            </li>
            <li class="nav-item" v-if="isLoggedIn()">
              <a class="nav-link" href="/logout">Logout</a>
            </li>
            <li class="nav-item dropdown">
              <a
                class="nav-link dropdown-toggle"
                href="#"
                id="navbarDropdown"
                role="button"
                data-bs-toggle="dropdown"
                aria-expanded="false"
              >
                Dropdown
              </a>
              <ul class="dropdown-menu" aria-labelledby="navbarDropdown">
                <li><a class="dropdown-item" v-if="isLoggedIn()" href="/posts/new">Create Post</a></li>
                <li><a class="dropdown-item" href="/about">About</a></li>
                <div v-if="!isLoggedIn()">
                  <li><hr class="dropdown-divider" /></li>
                  <li><a class="dropdown-item" href="/signup">Sign Up</a></li>
                </div>
              </ul>
            </li>
            <li class="nav-item" v-if="!isLoggedIn()">
              <a class="nav-link disabled">Welcome Guest</a>
            </li>
          </ul>
          <form class="d-flex">
            <input class="form-control me-2" type="search" placeholder="Search" aria-label="Search" />
            <button class="btn btn-outline-success" type="submit">Search</button>
          </form>
        </div>
      </div>
    </nav>
    <router-view />
  </div>
</template>

<style>
h1 {
  font-family: Impact, Haettenschweiler, "Franklin Gothic Bold", Charcoal, "Helvetica Inserat",
    "Bitstream Vera Sans Bold", "Arial Black", "sans serif";
  font-size: 24px;
  font-style: normal;
  font-variant: normal;
  font-weight: 700;
  line-height: 26.4px;
}
p {
  font-family: "Book Antiqua", Palatino, "Palatino Linotype", "Palatino LT STD", Georgia, serif;
  font-size: 14px;
  font-style: normal;
  font-variant: normal;
  font-weight: 400;
  line-height: 20px;
}
body {
  background-image: url("./assets/double-bubble.png");
}
</style>

<script>
export default {
  methods: {
    isLoggedIn: function () {
      if (localStorage.getItem("jwt")) {
        return true;
      } else {
        return false;
      }
    },
    getUserId: function () {
      return localStorage.getItem("user_id");
    },
  },
};
</script>
