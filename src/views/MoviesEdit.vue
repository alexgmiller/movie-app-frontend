<template>
  <div>
    <form v-on:submit.prevent="movieUpdate(movie)">
      Title:
      <input type="text" v-model="editMovieParams.title" />
      Plot:
      <input type="text" v-model="editMovieParams.plot" />
      Year:
      <input type="text" v-model="editMovieParams.year" />
      <br />
      <input type="submit" value="Update" />
      <button v-on:click="movieDestroy(movie)">DESTROY</button>
    </form>
  </div>
</template>

<script>
import axios from "axios";
export default {
  data: function () {
    return {
      editMovieParams: {},
      movie: {},
      errors: {},
    };
  },
  created: function () {
    axios.get("/movies/" + this.$route.params.id + ".json").then((response) => {
      console.log("Updated Movie", response.data);
      this.movie = response.data;
      this.editMovieParams = this.movie;
    });
  },
  methods: {
    movieUpdate: function (movie) {
      axios
        .patch("/movies/" + movie.id + ".json", this.editMovieParams)
        .then((response) => {
          console.log("Movie updated", response.data);
          this.$router.push("/movies");
        })
        .catch((error) => {
          console.log("Error on update attempt", error.response);
          this.errors = error.response.data.errors;
        });
    },
    movieDestroy: function (movie) {
      axios.delete("/movies/" + movie.id + ".json").then((response) => {
        console.log("Forever gone", response.data);
        this.$router.push("/movies");
      });
    },
  },
};
</script>
