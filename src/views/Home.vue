<script>
import axios from "axios";
export default {
  data: function () {
    return {
      message: "M O V I E S",
      movies: [],
      movie: {},
      editMovieParams: {},
    };
  },
  created: function () {
    this.indexMovies();
  },
  methods: {
    indexMovies: function () {
      console.log("sanity check");
      axios
        .get("/movies")
        .then((response) => {
          console.log(response.data);
          this.movies = response.data;
        })
        .catch((error) => console.log(error.response.data.errors));
    },
    showMovie: function (movie) {
      console.log(movie);
      this.movie = movie;
      this.editMovieParams = movie;
      document.querySelector("#more-info").showModal();
    },
    updateMovie: function (movie) {
      console.log(movie);
      axios
        .patch(`/movies/${movie.id}`, movie)
        .then((response) => {
          console.log(response.data);
        })
        .catch((error) => console.log(error.response.data.errors));
    },
    destroyMovie: function (movie) {
      // confirm method asks user using the browser for deletion confirmation
      if (confirm("Are you sure you want to delete this?")) {
        console.log(movie);
        axios
          .delete(`/movies/${movie.id}`, movie)
          .then((response) => {
            console.log(response.data.message);
            var index = this.movies.indexOf(movie);
            this.movies.splice(index, 1);
          })
          .catch((error) => console.log(error.response.data.errors));
      }
    },
  },
};
</script>

<template>
  <div class="home">
    <h1>{{ message }}</h1>
    <div v-for="movie in movies" v-bind:key="movie.id">
      <p>{{ movie.title }}</p>
      <button v-on:click="showMovie(movie)">More Info</button>
    </div>
    <div>
      <dialog id="more-info">
        <form method="dialog">
          <h1>{{ movie.title }}</h1>
          <p>
            Year:
            <br />
            {{ movie.year }}
          </p>
          <p>
            Summary:
            <br />
            {{ movie.plot }}
          </p>
          <p>
            Director(s):
            <br />
            {{ movie.director }}
          </p>
          <p>
            English?
            <br />
            {{ movie.english }}
          </p>
          <br />
          <h2>Edit Below</h2>
          <p>
            Year:
            <input type="text" v-model="movie.year" />
          </p>
          <p>
            Summary:
            <input type="text" v-model="movie.plot" />
          </p>
          <p>
            Director(s):
            <input type="text" v-model="movie.director" />
          </p>
          <p>
            English?
            <input type="text" v-model="movie.english" />
          </p>
          <button v-on:click="updateMovie(movie)">Update</button>
          <button v-on:click="destroyMovie(movie)">Delete</button>
          <button>Exit</button>
        </form>
      </dialog>
    </div>
  </div>
</template>

<!-- <style>
input[type="text"] {
  width: 500px;
  height: 20px;
}
</style> -->
