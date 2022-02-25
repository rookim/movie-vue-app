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
    <form class="d-flex">
      <input v-model="titleFilter" class="form-control me-2" type="search" placeholder="Search" list="titles" />
      <button class="btn btn-outline-success btn-dark" type="submit">Search</button>
    </form>
    <datalist id="titles">
      <option v-for="movie in movies" v-bind:key="movie.id">{{ movie.title }}</option>
    </datalist>
    <br />
    <br />

    <div class="row row-cols-1 row-cols-sm-2 row-cols-md-3 g-4">
      <div class="col" v-for="movie in filteredMovies" v-bind:key="movie.id">
        <div class="card h-100">
          <router-link v-bind:to="`/movies/${movie.id}`">
            <img
              src="https://thecinemaholic.com/wp-content/uploads/2021/01/nezuu-e1638963260523.jpg"
              class="card-img-top"
              alt="..."
            />
          </router-link>
          <div class="card-body">
            <h5 class="card-title">{{ movie.title }}</h5>
            <p class="card-text">
              {{ movie.plot }}
            </p>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>
