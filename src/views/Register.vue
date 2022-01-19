<template>
  <div>
    <h1>Register Page</h1>
    <form action="">
      <input type="text" placeholder="Username" v-model="this.Username" />
      <input type="text" placeholder="Email" v-model="this.Email" />
      <input type="text" placeholder="Password" v-model="this.Password" />
    </form>
    <button @click="registerUser()">Register Account</button>
  </div>
</template>

<script>
import axios from 'axios';

const baseURL = 'http://localhost:8000';

export default {
  name: 'Register',
  data() {
    return {
      Username: '',
      Email: '',
      Password: '',
    };
  },
  methods: {
    async registerUser() {
      try {
        await axios.post(`${baseURL}/api/register`, {
          Username: this.Username,
          Email: this.Email,
          Password: this.Password,
        });
      } catch (err) {
        console.log(err);
      }
    },
  },
};
</script>

<style scoped lang="scss"></style>
