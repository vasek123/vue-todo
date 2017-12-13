<template>
  <div id="app">
    <TodoList v-bind:todos="todos" />
  </div>
</template>

<script>
import TodoList from './components/TodoList';

export default {
  name: 'app',
  components: {
    TodoList,
  },
  data() {
    return {
      todos: [
        { id: 0, todo: 'Buy milk', isCompleted: true },
        { id: 1, todo: 'Prepare lunch', isCompleted: false },
      ],
    };
  },
};
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
