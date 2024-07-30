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
          this.$emit('add-task', this.task);
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
    background-color: #28a745;
    color: white;
    cursor: pointer;
  }
  
  button:hover {
    background-color: #218838;
  }
  
  button:active {
    background-color: #1e7e34;
  }
  </style>
  