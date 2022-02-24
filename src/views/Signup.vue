<script>
import axios from "axios";

export default {
  data: function () {
    return {
      newUserParams: { password: "", name: "" },
      errors: [],
    };
  },
  methods: {
    submit: function () {
      axios
        .post("/users", this.newUserParams)
        .then((response) => {
          console.log(response.data);
          this.$router.push("/login");
        })
        .catch((error) => {
          this.errors = error.response.data.errors;
        });
    },
  },
};
</script>

<template>
  <div class="signup">
    <form v-on:submit.prevent="submit()">
      <h1>Signup</h1>
      <ul>
        <li v-for="error in errors" v-bind:key="error">{{ error }}</li>
      </ul>
      <div>
        <label>Name:</label>
        <input type="text" v-model="newUserParams.name" />
        <br />
        <small v-if="newUserParams.name.length < 3">Must be at least 2 characters</small>
        <br />
        <small>{{ 25 - newUserParams.name.length }} characters remaining</small>
      </div>
      <br />
      <div>
        <label>Email:</label>
        <input type="email" v-model="newUserParams.email" />
      </div>
      <br />
      <div>
        <label>Password:</label>
        <input type="password" v-model="newUserParams.password" />
        <br />
        <small v-if="newUserParams.password.length < 8">Must be at least 8 characters</small>
        <small v-if="newUserParams.password.length > 20">Must be less than 20 characters</small>
      </div>
      <br />
      <div>
        <label>Password confirmation:</label>
        <input type="password" v-model="newUserParams.password_confirmation" />
      </div>
      <input type="submit" value="Submit" />
    </form>
  </div>
</template>
