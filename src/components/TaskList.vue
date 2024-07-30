<template>
    <ul>
      <TaskItem
        v-for="(task, index) in tasks"
        :key="index"
        :task="task"
        :index="index"
        @remove-task="removeTask"
        @toggle-task="toggleTask"
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
      }
    }
  }
  </script>
  
  <style scoped>
  ul {
    list-style-type: none;
    padding: 0;
  }
  </style>
  