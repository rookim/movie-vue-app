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
    <form action="" method="post">
      <ul>
        <li>
          <label for="title">Title</label>
          <input v-model="movieParams.title" type="text" id="title" />
        </li>
        <br />
        <li>
          <label for="year">Year</label>
          <input v-model="movieParams.year" type="text" id="year" />
        </li>
        <br />
        <li>
          <label for="plot">Plot</label>
          <input v-model="movieParams.plot" type="text" id="plot" />
          <br />
          <!-- use v-if directive if you don't want to display small tag right away -->
          <small>{{ 1000 - movieParams.plot.length }} characters remaining</small>
        </li>
        <br />
        <li>
          <label for="director">Director</label>
          <input v-model="movieParams.director" type="text" id="director" />
        </li>
        <br />
        <li>
          <label for="english">English</label>
          <input v-model="movieParams.english" type="text" id="english" />
        </li>
        <br />
        <li class="button">
          <button v-on:click="createMovie()" type="submit">Add movie</button>
        </li>
      </ul>
    </form>
  </div>
</template>

<style>
h1 {
  color: #18e9b1;
}
form {
  /* Center the form on the page */
  margin: 0 auto;
  width: 400px;
  /* Form outline */
  padding: 1em;
  border: 1px solid #ccc;
  border-radius: 3em;
}

ul {
  list-style: none;
  padding: 0em;
  width: 100%;
}

form li + li {
  margin-top: 1em;
}

input {
  width: 100%;
  max-width: 28em;
}

button {
  /* This extra margin represent roughly the same space as the space
     between the labels and their text fields */
  margin-left: 0.5em;
  background-color: #18e9b1; /* Green */
  border: none;
  color: white;
  padding: 15px 32px;
  text-align: center;
  text-decoration: none;
  display: inline-block;
  font-size: 16px;
}
</style>
