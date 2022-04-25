<template>
  <div>
    <h1>Make an add</h1>
    <form v-on:submit.prevent="movieCreate()">
      Title:
      <input type="text" v-model="newMovieParams.title" />
      Plot:
      <input type="text" v-model="newMovieParams.plot" maxlength="250" />
      Year:
      <input type="text" v-model="newMovieParams.year" />
    </form>
    <button v-on:click="movieCreate()">MAKE IT</button>
  </div>
</template>

<script>
import axios from "axios";
export default {
  data: function () {
    return {
      movies: {},
      newMovieParams: {},
      error: {},
    };
  },
  methods: {
    movieCreate: function () {
      axios
        .post("/movies.json", this.newMovieParams)
        .then((response) => {
          console.log("Movies Create", response.data);
          this.$router.push("/movies");
        })
        .catch((error) => {
          console.log("Error creating movie", error.response.data.errors);
        });
    },
  },
};
</script>
