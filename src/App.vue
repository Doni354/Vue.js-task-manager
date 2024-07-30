<template>
  <div id="app">
    <header>
      <h1>Task Manager</h1>
    </header>
    <main>
      <AddTask @add-task="addTask" />
      <TaskList :tasks="tasks" @remove-task="removeTask" @toggle-task="toggleTask" @edit-task="editTask" />
      <div class="actions">
        <button @click="removeCompletedTasks" class="remove-completed-btn">Hapus yang Dicentang</button>
      </div>
    </main>
  </div>
</template>

<script>
import AddTask from './components/AddTask.vue';
import TaskList from './components/TaskList.vue';
import { v4 as uuidv4 } from 'uuid';

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
    },
    removeCompletedTasks() {
      this.tasks = this.tasks.filter(task => !task.completed);
    }
  }
};
</script>

<style scoped>
#app {
  max-width: 800px;
  margin: 0 auto;
  padding: 20px;
  font-family: Arial, sans-serif;
  background-color: #f0f2f5;
  border-radius: 8px;
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
}

header {
  background-color: #007bff;
  padding: 10px 20px;
  border-radius: 8px 8px 0 0;
  color: white;
  text-align: center;
}

main {
  padding: 20px;
  background-color: white;
  border-radius: 0 0 8px 8px;
}

h1 {
  margin: 0;
}

.actions {
  margin-top: 20px;
  text-align: right;
}

.remove-completed-btn {
  padding: 10px 20px;
  background-color: #dc3545;
  border: none;
  border-radius: 4px;
  color: white;
  cursor: pointer;
}

.remove-completed-btn:hover {
  background-color: #c82333;
}

.remove-completed-btn:active {
  background-color: #bd2130;
}
</style>
