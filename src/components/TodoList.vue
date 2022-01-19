<template>
  <div>
    <h1>Todo List</h1>
    <!-- Create New todo -->
    <div>
      <form action="">
        <input type="text" placeholder="New Todo" v-model="this.newTodoText" />
        <button @click="newTodo()">New Todo</button>
      </form>
    </div>
    <!-- Create New todo -->
    <br />
    <!-- Get All todos -->
    <div>
      <button @click="getAllTodos()">Get All todos</button>
    </div>
    <!-- Get All todos -->
    <br />
    <!-- Get logged in users todos -->
    <div>
      <button @click="getSingleUsersTodos()">Get your todos</button>
    </div>
    <!-- Get logged in users todos -->
    <br />
    <!-- Listing of todos -->
    <div>
      <div v-for="todo of todos" :key="todo">
        <ul>
          <form action="">
            <input
              type="text"
              placeholder="Update Todo"
              v-model="this.updateTodoText"
            />
            <button @click="updateTodo(todo.id)">Update Todo</button>
          </form>
          <li>{{ todo.todo }}</li>
          <li>
            <button @click="updateTodoCompletion(todo.id, todo.completed)">
              {{ todo.completed }}
            </button>
          </li>
          <button @click="deleteTodo(todo.id)">Delete Todo</button>
        </ul>
      </div>
    </div>
    <!-- Listing of todos -->
  </div>
</template>

<script>
import axios from 'axios';

const baseURL = 'http://localhost:8000';

export default {
  name: 'TodoList',
  data() {
    return {
      todos: [],
      newTodoText: '',
      updateTodoText: '',
    };
  },
  methods: {
    async getAllTodos() {
      try {
        const token = localStorage.getItem('Token');
        const res = await axios.get(`${baseURL}/api/todos`, {
          headers: {
            'x-access-token': token,
          },
        });
        this.todos = res.data;
      } catch (err) {
        console.log(err);
      }
    },
    async getSingleUsersTodos() {
      let id = localStorage.getItem('userid');
      try {
        const token = localStorage.getItem('Token');
        const res = await axios.get(`${baseURL}/api/user/todos/${id}`, {
          headers: {
            'x-access-token': token,
          },
        });
        this.todos = res.data;
      } catch (err) {
        console.log(err);
      }
    },
    async deleteTodo(id) {
      try {
        const token = localStorage.getItem('Token');
        await axios.delete(`${baseURL}/api/todo/${id}`, {
          headers: {
            'x-access-token': token,
          },
        });
      } catch (err) {
        console.log(err);
      }
    },
    async newTodo() {
      try {
        const token = localStorage.getItem('Token');
        let id = localStorage.getItem('userid');
        let data = {
          todo: this.newTodoText.toString(),
          user_id: id.toString(),
        };
        if (!data.todo) {
          console.log('Todo is empty');
          return;
        } else {
          const res = await axios.post(`${baseURL}/api/todo`, data, {
            headers: {
              'x-access-token': token,
            },
          });
          console.log(res);
          console.log(this.newTodoText);
        }
      } catch (err) {
        console.log(err);
      }
    },
    async updateTodo(id) {
      try {
        const token = localStorage.getItem('Token');
        let data = { todo: this.updateTodoText.toString() };

        await axios.patch(`${baseURL}/api/todo/${id}`, data, {
          headers: {
            'x-access-token': token,
          },
        });
      } catch (err) {
        console.log(err);
      }
    },
    async updateTodoCompletion(id, completed) {
      const token = localStorage.getItem('Token');
      // var booleanValue = booleanValue ?? !booleanValue;
      let data = { completed: !completed };

      console.log(`Value is: ${data.completed}`);
      try {
        await axios.patch(`${baseURL}/api/todo/${id}`, data, {
          headers: {
            'x-access-token': token,
          },
        });
      } catch (err) {
        console.log(err);
      }
    },
  },
  created() {},
};
</script>

<style lang="scss" scoped>
ul {
  li {
    list-style: none;
  }
}
</style>
