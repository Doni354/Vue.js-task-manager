<template>
  <div id="app">
    <h1>Task Manager</h1>
    <AddTask @add-task="addTask" />
    <TaskList :tasks="tasks" @remove-task="removeTask" @toggle-task="toggleTask" />
  </div>
</template>

<script>
import AddTask from './components/AddTask.vue'
import TaskList from './components/TaskList.vue'

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
    addTask(task) {
      this.tasks.push(task);
    },
    removeTask(index) {
      this.tasks.splice(index, 1);
    },
    toggleTask(index) {
      this.tasks[index].completed = !this.tasks[index].completed;
    }
  }
}
</script>

<style scoped>
h1 {
  text-align: center;
}
</style>
