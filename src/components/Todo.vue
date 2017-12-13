<template>
  <div class="todo">
    <span>{{ todo }}</span><br />
    <small>is {{ isCompleted ? '' : 'not' }} completed</small>
  </div>
</template>

<script>
export default {
  name: 'Todo',
  props: ['todo', 'isCompleted'],
};
</script>

<style>

</style>


