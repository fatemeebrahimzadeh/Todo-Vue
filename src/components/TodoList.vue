<script setup>
import TodoTask from '@/components/TodoTask.vue'
import { computed, onMounted, ref, watch, watchEffect } from 'vue'
const props = defineProps(['taskList', 'todoListMode'])
import draggable from 'vuedraggable'
defineEmits(['deleteTask', 'checkTask', 'updateTodos'])

const todoList = ref([])

watch(
  () => props.taskList,
  (newInput) => {
    todoList.value.push(newInput)
  }
)

function deleteTask(index) {
  todoList.value.splice(index, 1)
}

function checkTask(index) {
  todoList.value[index].isTaskDone = !todoList.value[index].isTaskDone
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
  return (isTaskDone) => {
    if (props.todoListMode === 'completed') {
      return isTaskDone
    } else if (props.todoListMode === 'not-completed') {
      return !isTaskDone
    } else {
      return true
    }
  }
})
</script>

<template>
  <draggable class="content-container" v-model="todoList" tag="ul" itemKey="id">
    <template #item="{ element: { task, taskTime, isTaskDone }, index }">
      <transition name="fade">
        <todo-task
          v-if="listType(isTaskDone)"
          :task="task"
          :taskTime="taskTime"
          :isTaskDone="isTaskDone"
          @deleteTask="deleteTask(index)"
          @checkTask="checkTask(index)"
        />
      </transition>
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
