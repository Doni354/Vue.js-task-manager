<template>
    <li :class="{ completed: localTask.completed }">
      <input type="checkbox" v-model="localTask.completed" @change="toggleTask" />
      <span>{{ localTask.text }}</span>
      <button @click="removeTask">Remove</button>
    </li>
  </template>
  
  <script>
  export default {
    props: ['task', 'index'],
    data() {
      return {
        localTask: { ...this.task } // Copy props to local data
      };
    },
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
  