<template>
  <div>
    <h1>Login Page</h1>
    <form action="">
      <input type="text" placeholder="Email" v-model="this.Email" />
      <input type="text" placeholder="Password" v-model="this.Password" />
    </form>
    <button @click="loginUser()">Login</button>
  </div>
</template>

<script>
import axios from 'axios';

const baseURL = 'http://localhost:8000';

export default {
  name: 'Login',
  data() {
    return {
      Email: '',
      Password: '',
    };
  },
  methods: {
    async loginUser() {
      try {
        const res = await axios.post(`${baseURL}/api/login`, {
          Email: this.Email,
          Password: this.Password,
        });
        localStorage.setItem('Token', res.data.token);
        localStorage.setItem('userid', res.data.userid);
        this.$router.push('/');
      } catch (err) {
        console.log(err);
      }
    },
    persist() {
      localStorage.Token;
      console.log('Token saved to LocalStorage');
    },
  },
  mounted() {
    if (localStorage.Token) {
      this.Token = localStorage.Token;
    }
  },
  watch: {
    Token(newToken) {
      localStorage.Token = newToken;
    },
  },
  created() {},
};
</script>

<style scoped lang="scss"></style>
