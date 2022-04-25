<template>
  <nav>
    <router-link to="/">Home</router-link>
    |
    <router-link to="/movies">Movies</router-link>
    |
    <router-link to="/movies/new">Add Movie</router-link>
    |
    <span v-if="isLoggedIn()">
      <router-link to="/logout">Log Out</router-link>
      |
    </span>
    <span v-else>
      <router-link to="/signup">Sign Up</router-link>
      |
      <router-link to="/login">Log In</router-link>
      |
    </span>
    <router-link to="/about">About</router-link>
    |
  </nav>
  <router-view />
</template>

<script>
export default {
  data: function () {
    return {};
  },
  methods: {
    isLoggedIn: function () {
      return localStorage.getItem("jwt");
    },
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
nav {
  padding: 30px;
}
nav a {
  font-weight: bold;
  color: #2c3e50;
}
nav a.router-link-exact-active {
  color: #42b983;
}
</style>
