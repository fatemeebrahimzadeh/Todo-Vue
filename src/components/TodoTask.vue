<script setup>
// import { ref } from 'vue'

defineProps(['task', 'taskTime', 'isTaskDone'])
defineEmits(['deleteTask', 'checkTask'])
// let checkbox = ref(false)
</script>

<template>
  <div class="task-container drag-handle" :class="{ 'task--done': isTaskDone }">
    <span class="task__priority"></span>
    <div class="task__name">{{ task }}</div>
    <div class="task__time">{{ taskTime }}</div>
    <i class="task__delete fa-solid fa-close" @click.prevent="$emit('deleteTask')"></i>
    <input
      class="task__checkbox"
      type="checkbox"
      :checked="isTaskDone"
      @click="$emit('checkTask')"
    />
  </div>
</template>

<style scoped>
.task-container {
  background-color: white;
  border-radius: 20px;
  padding: 0.25rem 0.5rem;
  margin: 0.5rem;
  display: grid;
  grid-template-areas:
    'task__priority task__name task__delete task__checkbox'
    'task__priority task__time task__delete task__checkbox';
  grid-template-columns: 1fr 5fr 1fr;
  grid-template-rows: 1fr 1fr;
}

.drag-handle {
  cursor: move;
  /* Add additional styling as needed */
}

.task-container.task--done {
  background-color: #5f9ea06a;
}

.task-container.task--done .task__name,
.task-container.task--done .task__time {
  color: white;
  text-decoration: line-through;
}

.task-container .task__priority {
  background-color: var(--secondary);
  border-radius: 10px;
  margin: 0.5rem 0.25rem;
  grid-column-start: 1;
  grid-row: 1 / 3;
}

.task-container .task__name {
  margin: 0 0.25rem;
  grid-column-start: 2;
  grid-row: 1 / 2;
  max-width: 150px;
  white-space: nowrap;
  overflow: hidden;
  text-overflow: ellipsis;
}

.task-container .task__time {
  margin: 0 0.25rem;
  grid-column-start: 2;
  grid-row: 2 / 3;
  max-width: 150px;
  white-space: nowrap;
  overflow: hidden;
  text-overflow: ellipsis;
}

.task-container .task__delete {
  cursor: pointer;
  display: flex;
  justify-content: center;
  align-items: center;
  grid-column-start: 3;
  grid-row: 1 / 3;
}

.task-container .task__checkbox {
  display: flex;
  justify-content: center;
  align-items: center;
  grid-column-start: 4;
  grid-row: 1 / 3;
}
</style>
