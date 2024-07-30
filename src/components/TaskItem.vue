<template>
    <li :class="{ completed: localTask.completed }">
      <input type="checkbox" v-model="localTask.completed" @change="toggleTask" />
      <span v-if="!isEditing" @dblclick="editTask">{{ localTask.text }}</span>
      <input v-else v-model="newText" @keyup.enter="saveTask" @blur="saveTask" />
      <button @click="removeTask">Remove</button>
      <button @click="startEditing">Edit</button>
    </li>
  </template>
  
  <script>
  export default {
    props: ['task', 'index'],
    data() {
      return {
        localTask: { ...this.task },
        isEditing: false,
        newText: this.task.text,
      };
    },
    methods: {
      removeTask() {
        this.$emit('remove-task', this.index);
      },
      toggleTask() {
        this.$emit('toggle-task', this.index);
      },
      startEditing() {
        this.isEditing = true;
        this.newText = this.localTask.text;
      },
      saveTask() {
        if (this.newText.trim()) {
          this.isEditing = false;
          this.localTask.text = this.newText;
          this.$emit('edit-task', this.index, this.newText);
        }
      },
    }
  }
  </script>
  
  <style scoped>
  li {
    display: flex;
    align-items: center;
    justify-content: space-between;
    padding: 10px;
    border-bottom: 1px solid #ddd;
  }
  
  .completed span {
    text-decoration: line-through;
    color: #aaa;
  }
  
  input[type="text"] {
    flex: 1;
    margin-right: 10px;
    padding: 5px;
    border: 1px solid #ddd;
    border-radius: 4px;
  }
  
  button {
    margin-left: 5px;
    padding: 5px 10px;
    border: none;
    border-radius: 4px;
    cursor: pointer;
  }
  
  button:hover {
    background-color: #f0f0f0;
  }
  
  button:active {
    background-color: #ddd;
  }
  </style>
  