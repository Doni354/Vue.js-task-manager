<template>
    <ul>
      <TaskItem
        v-for="task in tasks"
        :key="task.id"
        :task="task"
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
      removeTask(id) {
        this.$emit('remove-task', id);
      },
      toggleTask(id) {
        this.$emit('toggle-task', id);
      },
      editTask(id, newText) {
        this.$emit('edit-task', id, newText);
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
  