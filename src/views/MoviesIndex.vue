<template>
  <h1>Look at all those movies!</h1>
  <div v-for="movie in movies" :key="movie.id">
    <h2>{{ movie.title }}</h2>
    <p>{{ movie.plot }}</p>
    <h4>Released: {{ movie.year }}</h4>
    <button>
      <router-link v-bind:to="`/movies/${movie.id}`">More Details</router-link>
    </button>
  </div>
</template>

<script>
import axios from "axios";
export default {
  data: function () {
    return {
      movies: {},
    };
  },
  created: function () {
    this.movieIndex();
  },
  methods: {
    movieIndex: function () {
      axios.get("/movies.json").then((response) => {
        this.movies = response.data;
        console.log("Movies index", response.data);
      });
    },
  },
};
</script>
