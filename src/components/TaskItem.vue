<template>
    <li :class="{ completed: localTask.completed }">
      <input type="checkbox" v-model="localTask.completed" @change="toggleTask" />
      <span v-if="!isEditing" @dblclick="startEditing" class="task-text">{{ localTask.text }}</span>
      <input v-else v-model="newText" @keyup.enter="saveTask" @blur="saveTask" />
      <small>{{ localTask.timestamp }}</small>
      <div class="task-actions">
        <button @click="removeTask">Remove</button>
        <button @click="startEditing">Edit</button>
      </div>
    </li>
  </template>
  
  <script>
  export default {
    props: ['task'],
    data() {
      return {
        localTask: { ...this.task },
        isEditing: false,
        newText: this.task.text,
      };
    },
    methods: {
      removeTask() {
        this.$emit('remove-task', this.task.id);
      },
      toggleTask() {
        this.$emit('toggle-task', this.task.id);
      },
      startEditing() {
        this.isEditing = true;
        this.newText = this.localTask.text;
      },
      saveTask() {
        if (this.newText.trim()) {
          this.isEditing = false;
          this.localTask.text = this.newText;
          this.$emit('edit-task', this.task.id, this.newText);
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
    transition: background-color 0.3s;
    word-wrap: break-word;
  }
  
  li:hover {
    background-color: #f1f1f1;
  }
  
  .completed .task-text {
    text-decoration: line-through;
    color: #aaa;
  }
  
  .task-text {
    flex: 1;
    overflow: hidden;
    text-overflow: ellipsis;
    white-space: nowrap;
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
    background-color: #007bff;
    color: white;
  }
  
  button:hover {
    background-color: #0056b3;
  }
  
  button:active {
    background-color: #003f7f;
  }
  
  small {
    color: #888;
    font-size: 0.8em;
    margin-left: 10px;
  }
  
  .task-actions {
    display: flex;
    gap: 5px;
  }
  </style>
  