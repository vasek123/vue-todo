<template>
  <div id="app">
    <span>Number of active todos: {{ numberOfActiveTodos }}</span>
    <button @click="newTodo">New todo</button>
    <button @click="archiveCompleted">Archive completed</button>
    <TodoList :todos="todos" @todo-new="newTodo" />
  </div>
</template>

<script>
import Vue from 'vue';
import TodoList from './components/TodoList';

export default {
  name: 'app',
  components: {
    TodoList,
  },

  data() {
    return {
      todos: {
        0: { id: 0, text: 'Buy milk', isCompleted: true },
        1: { id: 1, text: 'Prepare lunch', isCompleted: false },
      },
    };
  },

  computed: {
    numberOfActiveTodos: function () {
      return Object.values(this.todos).filter(todo => !todo.isCompleted).length;
    }
  },

  methods: {
    newTodo: function () {
      let maxIndex = Object.keys(this.todos).reduce((a, b, ) => Math.max(a, b), 0);
      let newIndex = maxIndex + 1;

      Vue.set(this.todos, newIndex, {
        id: newIndex,
        text: `Todo #${Object.keys(this.todos).length + 1}`,
        isCompleted: false,
      });
    },

    saveTodo: function (id, editedText) {
      this.todos[id].text = editedText;
    },

    removeTodo: function (id) {
      Vue.delete(this.todos, id);
    },

    archiveCompleted: function () {
      for (let id in this.todos) {
        if (this.todos[id].isCompleted) Vue.delete(this.todos, id);
      }
    },
  },

  created() {
    bus.$on('todo-save', this.saveTodo);
    bus.$on('todo-remove', this.removeTodo);
  }
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
