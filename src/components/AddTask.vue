<template>
    <div class="add-task">
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
  .add-task {
    display: flex;
    justify-content: space-between;
    margin-bottom: 20px;
  }
  
  input {
    flex: 1;
    padding: 10px;
    border: 1px solid #ddd;
    border-radius: 4px;
    margin-right: 10px;
  }
  
  button {
    padding: 10px;
    border: none;
    border-radius: 4px;
    background-color: #007bff;
    color: white;
    cursor: pointer;
  }
  
  button:hover {
    background-color: #0056b3;
  }
  
  button:active {
    background-color: #003f7f;
  }
  </style>
  