<template>
  <div class="todo">
    <div v-show="!isBeingEdited">
      <span :class="{ completed: todo.isCompleted }">{{ todo.text }}</span><br />
      <small>is {{ todo.isCompleted ? '' : 'not' }} completed</small>
      <input type="checkbox" v-model="todo.isCompleted">
      <button @click="edit">Edit</button>
      <button @click="remove">Remove</button>
    </div>

    <div v-show="isBeingEdited">
      <input type="text" v-model="editedText" />
      <button @click="save">Save</button>
      <button @click="cancelEdit">Cancel</Button>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Todo',
  props: ['todo'],

  data() {
    return {
      isBeingEdited: false,
      editedText: '',
    }
  },

  methods: {
    edit: function () {
      this.isBeingEdited = true;
      this.editedText = this.todo.text;
    },
    
    cancelEdit: function () {
      this.isBeingEdited = false;
      this.editedText = '';
    },

    save: function () {
      bus.$emit('todo-save', this.todo.id, this.editedText)
      this.isBeingEdited = false;
      this.editedText = '';

    },

    remove: function () {
      bus.$emit('todo-remove', this.todo.id);
    },
  }
};
</script>

<style scoped>
  .completed {
    text-decoration: line-through;
  }
</style>
