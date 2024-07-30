<template>
  <div id="app">
    <h1>Task Manager</h1>
    <AddTask @add-task="addTask" />
    <TaskList :tasks="tasks" @remove-task="removeTask" @toggle-task="toggleTask" @edit-task="editTask" />
  </div>
</template>

<script>
import AddTask from './components/AddTask.vue'
import TaskList from './components/TaskList.vue'
import { v4 as uuidv4 } from 'uuid'; // Import UUID for unique IDs

export default {
  components: {
    AddTask,
    TaskList,
  },
  data() {
    return {
      tasks: [],
    };
  },
  methods: {
    addTask(taskText) {
      const newTask = {
        id: uuidv4(),
        text: taskText,
        completed: false,
        timestamp: new Date().toLocaleString(),
      };
      this.tasks.push(newTask);
    },
    removeTask(id) {
      this.tasks = this.tasks.filter(task => task.id !== id);
    },
    toggleTask(id) {
      const task = this.tasks.find(task => task.id === id);
      task.completed = !task.completed;
    },
    editTask(id, newText) {
      const task = this.tasks.find(task => task.id === id);
      task.text = newText;
    }
  }
}
</script>

<style scoped>
#app {
  max-width: 600px;
  margin: 0 auto;
  padding: 20px;
  font-family: Arial, sans-serif;
}

h1 {
  text-align: center;
  color: #333;
}
</style>
