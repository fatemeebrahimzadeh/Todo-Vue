<script setup>
import TodoTask from '@/components/TodoTask.vue'
import { computed, onMounted, ref, watch, watchEffect } from 'vue'
const props = defineProps(['inputData', 'listMode'])
import draggable from 'vuedraggable'
defineEmits(['deleteTask', 'checkTask', 'updateTodos'])

const todoList = ref([])

watch(
  () => props.inputData,
  (newInput) => {
    todoList.value.push(newInput)
  }
)

function deleteTask(index) {
  todoList.value.splice(index, 1)
}

function checkTask(index) {
  todoList.value[index].isChecked = !todoList.value[index].isChecked
}

onMounted(() => {
  const storedData = localStorage.getItem('todoList')
  if (storedData) {
    todoList.value = JSON.parse(storedData)
  }
})

watchEffect(() => {
  localStorage.setItem('todoList', JSON.stringify(todoList.value))
})

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
  <draggable class="content-container" v-model="todoList" tag="ul" itemKey="id">
    <template #item="{ element: { task, time, isChecked }, index }">
      <todo-task
        v-if="listType(isChecked)"
        :task="task"
        :time="time"
        :isChecked="isChecked"
        @deleteTask="deleteTask(index)"
        @checkTask="checkTask(index)"
      />
    </template>
  </draggable>
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
    max-height: 500px;
  }
}
</style>
