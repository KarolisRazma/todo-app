<script setup lang="ts">
import { ref } from 'vue'

const emit = defineEmits<{
  newTodo: [title: string]
}>()

const todoTitle = ref<string>('')
const handleOnSubmit = () => {
  emit('newTodo', todoTitle.value)
  todoTitle.value = '' // Clear input field
}
</script>

<template>
  <form @submit.prevent="handleOnSubmit">
    <label for="todo-title"> Provide todo title: </label>
    <br />
    <input v-model.trim="todoTitle" type="text" id="todo-title" name="todo-title" required />
    <br />
    <button type="submit">Add</button>
  </form>
</template>

<style scoped>
label {
  font-size: 1.1rem;
  color: #333;
}

input {
  padding: 10px;
  border: 1px solid #ccc;
  border-radius: 4px;
  font-size: 1rem;
  width: 100%;
}

input:focus {
  outline: none;
  border-color: #42b983;
  box-shadow: 0 0 5px rgba(66, 185, 131, 0.5);
}

button {
  padding: 10px 20px;
  background-color: #42b983;
  color: white;
  border: none;
  border-radius: 4px;
  font-size: 1rem;
  cursor: pointer;
  transition: background-color 0.3s ease;
}

button:hover {
  background-color: #369870;
}

form {
  display: flex;
  flex-direction: column;
  align-items: center;
}

form input[type='text'] {
  width: 100%;
  padding: 10px;
  margin-bottom: 10px;
  border: 1px solid #ccc;
  border-radius: 4px;
}

form button[type='submit'] {
  background-color: #42b983;
  color: white;
  border: none;
  border-radius: 4px;
  cursor: pointer;
  font-size: 1rem;
}

form button[type='submit']:hover {
  background-color: #369870;
}
</style>
