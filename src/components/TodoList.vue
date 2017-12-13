<template>
  <div class="todo-list">
    <span>Number of active todos: {{ numberOfActiveTodos }}</span>
    <Todo v-for="todo in todos" v-bind:key="todo.id" v-bind="todo"/>
  </div>  
</template>

<script>
import Todo from './Todo';

export default {
  name: 'TodoList',
  props: ['todos'],

  components: {
    Todo,
  },

  computed: {
    numberOfActiveTodos() {
      return this.todos.filter(todo => !todo.isCompleted).length;
    },
  },
};
</script>

<style>

</style>

