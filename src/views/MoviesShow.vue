<script>
import axios from "axios";

export default {
  data: function () {
    return {
      movie: {},
    };
  },
  created: function () {
    this.showMovie();
  },
  methods: {
    showMovie: function () {
      axios.get(`/movies/${this.$route.params.id}`).then((response) => {
        console.log("Movies Show", response.data);
        this.movie = response.data;
      });
    },
    destroyMovie: function () {
      axios
        .delete(`/movies/${this.movie.id}`)
        .then((response) => {
          console.log("Successfully deleted....", response.data);
        })
        .catch((error) => {
          console.log("Error", error.response.data.errors);
          this.errors = error.response.data.errors;
        });
    },
  },
};
</script>

<template>
  <div class="movies-show">
    <h1>{{ movie.title }}</h1>
    <p>Directed by {{ movie.director }}</p>
    <p>{{ movie.plot }}</p>
    <br />
    <button><router-link :to="`/movies/${movie.id}/edit`">Edit</router-link></button>
    <button v-on:click="destroyMovie()">Delete</button>
  </div>
</template>
