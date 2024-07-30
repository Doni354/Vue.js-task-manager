<template>
    <ul>
      <TaskItem
        v-for="(task, index) in tasks"
        :key="index"
        :task="task"
        :index="index"
        @remove-task="removeTask"
        @toggle-task="toggleTask"
        @edit-task="editTask"
      />
    </ul>
  </template>
  
  <script>
  import TaskItem from './TaskItem.vue'
  
  export default {
    components: {
      TaskItem
    },
    props: ['tasks'],
    methods: {
      removeTask(index) {
        this.$emit('remove-task', index);
      },
      toggleTask(index) {
        this.$emit('toggle-task', index);
      },
      editTask(index, newText) {
        this.$emit('edit-task', index, newText);
      }
    }
  }
  </script>
  
  <style scoped>
  ul {
    list-style-type: none;
    padding: 0;
    margin: 0;
  }
  </style>
  