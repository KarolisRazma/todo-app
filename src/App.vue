<script setup lang="ts">
import TodoDashboard from './views/TodoDashboard.vue'
</script>

<template>
  <div class="app-container">
    <TodoDashboard />
  </div>
</template>

<style scoped>
.app-container {
  max-width: 600px;
  margin: 50px auto;
  padding: 20px;
  background-color: #f9f9f9;
  border-radius: 8px;
  box-shadow: 0 4px 10px rgba(0, 0, 0, 0.1);
  text-align: center;
}
</style>
