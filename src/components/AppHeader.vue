<script setup>
defineEmits(['changeMode'])
</script>

<template>
  <header class="app-header">
    <h1>Todo List</h1>
    <nav>
      <button @click="$emit('changeMode', 'completed')" aria-label="Show completed tasks">
        completed list
      </button>
      <span> | </span>
      <button @click="$emit('changeMode', 'not-completed')" aria-label="Show not completed tasks">
        not completed list
      </button>
    </nav>
  </header>
</template>

<style scoped>
.app-header {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  font-weight: 600;
}

.app-header span {
  color: var(--secondary);
}
</style>
