<script>
import axios from "axios";

export default {
  data: function () {
    return {
      movieParams: { plot: "" },
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
    <br />
    <p>
      Year:
      <input v-model="movieParams.year" type="text" />
    </p>
    <br />
    <p>
      Plot:
      <input v-model="movieParams.plot" type="text" />
      <br />
      <!-- use v-if directive if you don't want to display small tag right away -->
      <small>{{ 1000 - movieParams.plot.length }} characters remaining</small>
    </p>
    <br />
    <p>
      Director:
      <input v-model="movieParams.director" type="text" />
    </p>
    <br />
    <p>
      English?
      <input v-model="movieParams.english" type="text" />
    </p>
    <button v-on:click="createMovie()" type="submit">Add movie</button>
  </div>
</template>
