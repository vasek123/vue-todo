<template>
  <div class="todo-list">
    <Todo v-for="todo in Object.values(todos)" :key="todo.id" :todo.sync="todo" />
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
      return Object.values(this.todos).filter(todo => !todo.isCompleted).length;
    },
  },

  methods: {
    newTodo: function () {
      this.$emit('todo-new');
    }
  }
};
</script>

<style>

</style>

