<template>
  <div>
    <img class="logo" src="../assets/logoResto.jpg" />
    <h1>Login</h1>
    <div class="register">
      <input type="text" v-model="email" placeholder="Enter Email" />

      <input type="password" v-model="password" placeholder="Enter Password" />

      <button v-on:click="Login">Login</button>
      <p>
        <router-link to="/signup">Sign Up</router-link>
      </p>
    </div>
  </div>
</template>
<script>
import axios from "axios";
export default {
  name: "Login",
  data() {
    return {
      email: "",
      password: "",
    };
  },
  methods: {
    async Login() {
      let result = await axios.get(
        `http://localhost:3000/users?email=${this.email}?password=${this.password}`
      );
      if (result.status == 200 && result.data.length > 0) {
        localStorage.setItem("user-info", JSON.stringify(result.data[0]));
        this.$router.push({ name: "Home" });
      }
      console.warn(result);
    },
  },
  mounted() {
    let user = localStorage.getItem("user-info");
    if (user) {
      this.$router.push({ name: "Home" });
    }
  },
};
</script>

<style>
</style>