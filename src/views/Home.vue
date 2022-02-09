<script>
export default {
  data: function () {
    return {
      message: "M O V I E S",
    };
  },
  created: function () {},
  methods: {
    indexMovies: function () {
      console.log("sanity check");
      axios.get();
    },
  },
};
</script>

<template>
  <div class="home">
    <h1>{{ message }}</h1>
    <button v-on:click="indexMovies()">View movies</button>
  </div>
</template>

<style></style>
