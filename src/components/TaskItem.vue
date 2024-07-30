<template>
    <li :class="{ completed: task.completed }">
      <input type="checkbox" v-model="task.completed" @change="toggleTask" />
      <span>{{ task.text }}</span>
      <button @click="removeTask">Remove</button>
    </li>
  </template>
  
  <script>
  export default {
    props: ['task', 'index'],
    methods: {
      removeTask() {
        this.$emit('remove-task', this.index);
      },
      toggleTask() {
        this.$emit('toggle-task', this.index);
      }
    }
  }
  </script>
  
  <style scoped>
  .completed span {
    text-decoration: line-through;
  }
  button {
    margin-left: 10px;
  }
  </style>
  