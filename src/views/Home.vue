<template>
  <div>
    <h1>Home Page</h1>
    <TodoList />
  </div>
</template>

<script>
import TodoList from '@/components/TodoList.vue';

export default {
  name: 'Home',
  components: {
    TodoList,
  },
};
</script>
