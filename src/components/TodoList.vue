<script setup lang="ts">
import type { Todo } from '@/models/Todo.model'

const props = defineProps({
  todos: {
    type: Array<Todo>,
    required: true
  }
})

const emit = defineEmits<{
  todoStatusChanged: [id: number]
  todoDeleted: [id: number]
}>()

const toggleTodoStatus = (id: number) => {
  emit('todoStatusChanged', id)
}

const handleTodoDelete = (id: number) => {
  emit('todoDeleted', id)
}
</script>

<template>
  <div
    v-for="{ id, title, isCompleted } in props.todos"
    :key="id"
    :class="{ completed: isCompleted }"
    class="todo-item"
  >
    <span>{{ title }}</span>
    <div class="button-group">
      <button v-if="!isCompleted" class="check-button" @click="toggleTodoStatus(id)">✓</button>
      <button v-else class="undo-button" @click="toggleTodoStatus(id)">↺</button>
      <button class="delete-button" @click="handleTodoDelete(id)">✕</button>
    </div>
  </div>
</template>

<style scoped>
.todo-item {
  padding: 15px;
  margin: 10px 0;
  background-color: #fff;
  border-radius: 6px;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.1);
  font-size: 1.2rem;
  display: flex;
  justify-content: space-between;
  align-items: center;
  transition:
    background-color 0.3s ease,
    color 0.3s ease;
}

.todo-item:hover {
  background-color: #f0f0f0;
}

.todo-item.completed {
  color: #bbb;
  background-color: #f3f3f3;
}

.button-group {
  display: flex;
  gap: 10px;
}

.check-button,
.undo-button,
.delete-button {
  background-color: #42b983;
  color: white;
  border: none;
  border-radius: 50%;
  width: 25px;
  height: 25px;
  display: flex;
  justify-content: center;
  align-items: center;
  cursor: pointer;
  font-size: 1.2rem;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.2);
}

.undo-button {
  background-color: #ffa500;
}

.undo-button:hover {
  background-color: #e69500;
}

.check-button:hover {
  background-color: #369870;
}

.delete-button {
  background-color: #ff4b4b;
}

.delete-button:hover {
  background-color: #d63c3c;
}
</style>
