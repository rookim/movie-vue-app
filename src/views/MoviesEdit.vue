<script>
import axios from "axios";

export default {
  data: function () {
    return {
      movie: {},
      errors: [],
    };
  },
  created: function () {
    axios.get(`/movies/${this.$route.params.id}`).then((response) => {
      console.log("Movies Index", response.data);
      this.movie = response.data;
    });
  },
  methods: {
    updateMovie: function () {
      axios
        .patch(`/movies/${this.$route.params.id}`, this.movie)
        .then((response) => {
          console.log("Successfully update!", response.data);
          this.movie = response.data;
        })
        .catch((error) => {
          console.log(error.response.data.errors);
          this.errors = error.response.data.errors;
        });
    },
  },
};
</script>

<template>
  <div class="movies-edit">
    <div v-for="error in errors" v-bind:key="error">
      <p>{{ error }}</p>
    </div>
    <form action="">
      <p>
        Title:
        <input v-model="movie.title" type="text" />
      </p>
      <p>
        Year:
        <input v-model="movie.year" type="text" />
      </p>
      <p>
        Plot:
        <input v-model="movie.plot" type="text" />
      </p>
      <p>
        Director:
        <input v-model="movie.director" type="text" />
      </p>
      <p>
        English?
        <input v-model="movie.english" type="text" />
      </p>
      <button v-on:click="updateMovie()">Update</button>
    </form>
    <br />
  </div>
</template>

<style></style>
