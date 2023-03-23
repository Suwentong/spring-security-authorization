
<template>
  <div>
    <h2>Login</h2>
    <form @submit.prevent="login">
      <div>
        <label for="email">Email:</label>
        <input type="text" id="email" v-model="email">
      </div>
      <div>
        <label for="password">Password:</label>
        <input type="password" id="password" v-model="password">
      </div>
      <button type="submit" @click="login">Login</button>
    </form>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  data() {
    return {
      email: "",
      password: "",
    };
  },
  methods: {
    async login() {
      try {
        const response = await axios.post("/api/v1/auth/authenticate", {
          email: this.email,
          password: this.password,
        });
        const token = response.data.token;
        localStorage.setItem("token", token);
        this.$router.push("api/v1/demo-controller");
      } catch (error) {
        console.log(error);
      }
    },
  },
};
</script>
