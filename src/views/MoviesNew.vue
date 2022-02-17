<script>
import axios from "axios";

export default {
  data: function () {
    return {
      movieParams: {},
      errors: [],
    };
  },
  created: function () {},
  methods: {
    createMovie: function () {
      axios
        .post("/movies", this.movieParams)
        .then((response) => {
          console.log("New Movie", response.data);
          this.movieParams = {};
          this.$router.push("/movies");
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
  <div class="movies-new">
    <h1>Add New Movie</h1>
    <div v-if="errors">
      <p v-for="error in errors" v-bind:key="error">{{ error }}</p>
    </div>
    <p>
      Title:
      <input v-model="movieParams.title" type="text" />
    </p>
    <p>
      Year:
      <input v-model="movieParams.year" type="text" />
    </p>
    <p>
      Plot:
      <input v-model="movieParams.plot" type="text" />
    </p>
    <p>
      Director:
      <input v-model="movieParams.director" type="text" />
    </p>
    <p>
      English?
      <input v-model="movieParams.english" type="text" />
    </p>
    <button v-on:click="createMovie()" type="submit">Add movie</button>
  </div>
</template>
