<template>
  <div class="todo-container">
    <h1>✅ To-Do List</h1>

    <form @submit.prevent="addTodo">
      <input
        v-model="newTask"
        type="text"
        placeholder="Add a new task..." 
      />
      <button type="submit">Add</button>
    </form>
    <ul class="task-list">
      <li
        v-for="(todo, index) in todos"
        :key="index"
        :class="{completed: todo.completed}"
      >
        <span @click="toggleTodo(index)">
          {{ todo.text }}
        </span>
        <button class="delete" @click="deleteTodo(index)">
          <DeleteIcon />
        </button>
      </li>
    </ul>

    <p v-if="todos.length === 0" class="empty-message">No tasks yet. Add one above 👆</p>
    
  </div>
</template>

<script setup>
import { ref } from 'vue';
import DeleteIcon from './DeleteIcon.vue'

const newTask = ref('');
const todos = ref([]);

const addTodo = () => {
  const trimmed = newTask.value.trim();
  if (trimmed) {
    todos.value.push({text: trimmed, completed: false});
    newTask.value = '';
  }
}

const deleteTodo = (index) => {
  todos.value.splice(index, 1);
}

const toggleTodo = (index) => {
  todos.value[index].completed = !todos.value[index].completed;
}

</script>