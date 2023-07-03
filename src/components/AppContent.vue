<script setup>
import TodoTask from '@/components/TodoTask.vue'
const props = defineProps(['todoList', 'listMode'])
defineEmits(['deleteTask', 'checkTask', 'todos-updated'])

const listType = (isChecked) => {
  if (props.listMode === 'completed') {
    return isChecked
  } else if (props.listMode === 'not-completed') {
    return !isChecked
  } else {
    return true
  }
}
</script>

<template>
  <div class="content-container">
    <template v-for="({ task, time, isChecked }, index) in todoList" :key="time.toString()">
      <transition name="fade">
        <todo-task
          v-if="listType(isChecked)"
          :task="task"
          :time="time"
          :isChecked="isChecked"
          @deleteTask="$emit('deleteTask', index)"
          @checkTask="$emit('checkTask', index)"
        />
      </transition>
    </template>
  </div>
</template>

<style scoped>
.content-container {
  overflow-y: auto;
}

.drag-handle {
  cursor: move;
  /* Add additional styling as needed */
}

.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.5s;
}

.fade-enter,
.fade-leave-to {
  opacity: 0;
}

@media (min-width: 640px) {
  .content-container {
    max-height: 400px;
  }
}
</style>
