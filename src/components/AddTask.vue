<template>
    <div>
      <input v-model="task" @keyup.enter="submitTask" placeholder="Add a new task" />
      <button @click="submitTask">Add Task</button>
    </div>
  </template>
  
  <script>
  export default {
    data() {
      return {
        task: ''
      };
    },
    methods: {
      submitTask() {
        if (this.task.trim()) {
          this.$emit('add-task', { text: this.task, completed: false });
          this.task = '';
        }
      }
    }
  }
  </script>
  
  <style scoped>
  input {
    width: 70%;
    padding: 10px;
  }
  button {
    padding: 10px;
  }
  </style>
  