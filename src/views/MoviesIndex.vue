<script>
import axios from "axios";

export default {
  data: function () {
    return {
      movies: [],
      titleFilter: "",
    };
  },
  created: function () {
    axios.get("/movies").then((response) => {
      console.log("Movies Index:", response.data);
      this.movies = response.data;
    });
  },
  function: {},
  computed: {
    filteredMovies() {
      return this.movies.filter((movie) => {
        return movie.title.toLowerCase().includes(this.titleFilter.toLowerCase());
      });
    },
  },
};
</script>

<template>
  <div class="movies-index">
    <p>
      Search by title:
      <input v-model="titleFilter" type="text" list="titles" />
    </p>
    <datalist id="titles">
      <option v-for="movie in movies" v-bind:key="movie.id">{{ movie.title }}</option>
    </datalist>
    <br />
    <br />
    <br />

    <div v-for="movie in filteredMovies" v-bind:key="movie.id">
      <router-link v-bind:to="`/movies/${movie.id}`">
        <p>{{ movie.title }}</p>
      </router-link>
      <br />
    </div>
  </div>
</template>
