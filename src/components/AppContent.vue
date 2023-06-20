<script setup>
import ContentTask from '@/components/ContentTask.vue'
import { computed } from 'vue'
const props = defineProps(['inputData', 'listMode'])
defineEmits(['deleteTask', 'checkTask'])

const listType = computed(() => {
  return (isChecked) => {
    if (props.listMode === 'completed') {
      return isChecked
    } else if (props.listMode === 'not-completed') {
      return !isChecked
    } else {
      return true
    }
  }
})
</script>

<template>
  <div class="content-container">
    <template v-for="({ task, time, isChecked }, index) in inputData" :key="time.toString()">
      <transition name="fade">
        <content-task
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
