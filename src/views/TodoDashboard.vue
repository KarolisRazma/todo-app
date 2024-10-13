<script setup lang="ts">
import { ref } from 'vue'
import type { Todo } from '@/models/Todo.model'
import TodoList from '@/components/TodoList.vue'
import TodoForm from '@/components/TodoForm.vue'

// todo: get these items from somewhere else
let lastId = 4
const todos = ref<Array<Todo>>([
  { id: 1, title: 'Item 1', isCompleted: false },
  { id: 2, title: 'Item 2', isCompleted: true },
  { id: 3, title: 'Item 3', isCompleted: false },
  { id: 4, title: 'Item 4', isCompleted: false }
])

const createNewTodo = (title: string) => {
  lastId++
  todos.value.push({ id: lastId, title, isCompleted: false })
  closeModal()
}

const removeTodo = (id: number) => {
  todos.value = todos.value.filter((todo) => todo.id !== id)
}

const changeTodoStatus = (id: number) => {
  const todo = todos.value.find((item) => item.id === id)
  if (todo) {
    todo.isCompleted = !todo.isCompleted
  }
}

const showModal = ref<boolean>(false)
const openModal = () => {
  showModal.value = true
}

const closeModal = () => {
  showModal.value = false
}
</script>

<template>
  <h1 class="todo-header">Todo Dashboard</h1>
  <button @click="openModal" class="open-modal-button">Add New Todo</button>
  <TodoList :todos @todo-status-changed="changeTodoStatus" @todo-deleted="removeTodo" />

  <div v-if="showModal" class="modal-overlay" @click="closeModal">
    <div class="modal-content" @click.stop>
      <button class="close-button" @click="closeModal">×</button>
      <TodoForm @new-todo="createNewTodo" />
    </div>
  </div>
</template>

<style scoped>
.todo-header {
  font-size: 2rem;
  margin-bottom: 20px;
  color: #1a4733;
}

.open-modal-button {
  padding: 10px 20px;
  background-color: #42b983;
  color: white;
  border: none;
  border-radius: 4px;
  cursor: pointer;
  font-size: 1rem;
}

.open-modal-button:hover {
  background-color: #369870;
}

.modal-overlay {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, 0.5);
  display: flex;
  justify-content: center;
  align-items: center;
  z-index: 1000;
  overflow: hidden;
}

.modal-content {
  background-color: white;
  padding: 20px;
  border-radius: 8px;
  box-shadow: 0 4px 10px rgba(0, 0, 0, 0.1);
  width: 100%;
  max-width: 400px;
  position: relative;
  margin: 0 20px;
  box-sizing: border-box;
  text-align: center;
}

.close-button {
  position: absolute;
  top: 10px;
  right: 10px;
  background: none;
  border: none;
  font-size: 1.5rem;
  cursor: pointer;
}

.close-button:hover {
  color: #ff4b4b;
}
</style>
