<script>
import axios from "axios";

export default {
  data: function () {
    return {
      movies: [],
    };
  },
  created: function () {
    axios.get("/movies").then((response) => {
      console.log("Movies Index:", response.data);
      this.movies = response.data;
    });
  },
  function: {},
};
</script>

<template>
  <div class="movies-index">
    <div v-for="movie in movies" v-bind:key="movie.id">
      <router-link v-bind:to="`/movies/${movie.id}`">
        <p>{{ movie.title }}</p>
      </router-link>
      <br />
    </div>
  </div>
</template>
