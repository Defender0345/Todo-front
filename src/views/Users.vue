<template>
  <div class="about">
    <h1>Check and update Users</h1>
    <br />
    <!-- Find User By ID -->
    <div>
      <input
        type="text"
        placeholder="Find User by ID"
        v-model="this.findUserInput"
      />
      <button @click="findUserByID()">Find User</button>
      <div>
        <li v-for="value in findUser" :key="value">{{ value[0].Username }}</li>
        <li v-for="value in findUser" :key="value">{{ value[0].Email }}</li>
        <li v-for="value in findUser" :key="value">{{ value[0].user_id }}</li>
      </div>
    </div>
    <!-- Find User By ID -->
    <br />
    <!-- Delete user by ID -->
    <div>
      <input
        type="text"
        placeholder="Delete User by ID"
        v-model="this.deleteUserInput"
      />
      <button @click="deleteUserByID()">Delete User</button>
    </div>
    <!-- Delete user by ID -->
    <br />
    <!-- Get All users -->
    <div>
      <button @click="getAllUsers()">Get All Users</button>
      <div v-for="user of users" :key="user">
        <ul>
          <li>{{ user.Username }}</li>
          <li>{{ user.Email }}</li>
        </ul>
      </div>
    </div>
    <!-- Get All users -->
  </div>
</template>

<script>
import axios from 'axios';

const baseURL = 'http://localhost:8000';

export default {
  name: 'Users',
  data() {
    return {
      users: [],
      findUserInput: '',
      findUser: [],
      deleteUserInput: '',
    };
  },
  methods: {
    async getAllUsers() {
      try {
        const token = localStorage.getItem('Token');
        const res = await axios.get(`${baseURL}/api/users`, {
          headers: {
            'x-access-token': token,
          },
        });
        this.users = res.data;
      } catch (err) {
        console.log(err);
      }
    },
    async findUserByID() {
      try {
        const token = localStorage.getItem('Token');
        const res = await axios.get(
          `${baseURL}/api/user/${this.findUserInput}`,
          {
            headers: {
              'x-access-token': token,
            },
          }
        );
        this.findUser = res.data;
      } catch (err) {
        console.log(err);
      }
    },
    async deleteUserByID() {
      try {
        const token = localStorage.getItem('Token');
        await axios.delete(`${baseURL}/api/user/${this.deleteUserInput}`, {
          headers: {
            'x-access-token': token,
          },
        });
        localStorage.removeItem('Token');
      } catch (err) {
        console.log(err);
      }
    },
  },
};
</script>

<style lang="scss" scoped>
li {
  list-style: none;
}
</style>
