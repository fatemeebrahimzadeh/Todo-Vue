<script setup>
import { reactive, ref } from 'vue'
import AppHeader from '@/components/AppHeader.vue'
import AppContent from '@/components/AppContent.vue'
import AppEntrance from '@/components/AppEntrance.vue'

const storageAvailable = typeof window !== 'undefined' && typeof window.localStorage !== 'undefined'

let storedTodoList = []
if (storageAvailable) {
  const storedData = localStorage.getItem('todoList')
  storedTodoList = storedData ? JSON.parse(storedData) : []
}

const todoList = reactive(storedTodoList)
const listMode = ref('')

function submit(data) {
  todoList.push({ task: data, time: new Date(), isChecked: false })
  if (storageAvailable) {
    localStorage.setItem('todoList', JSON.stringify(todoList))
  }
}

function deleteTask(index) {
  todoList.splice(index, 1)
  if (storageAvailable) {
    localStorage.setItem('todoList', JSON.stringify(todoList))
  }
}

function checkTask(index) {
  todoList[index].isChecked = !todoList[index].isChecked
  if (storageAvailable) {
    localStorage.setItem('todoList', JSON.stringify(todoList))
  }
}

function changeMode(mode) {
  listMode.value = mode
}
</script>

<template>
  <div class="container">
    <app-header @changeMode="changeMode" />
    <app-content
      :todoList="todoList"
      @deleteTask="deleteTask"
      @checkTask="checkTask"
      :listMode="listMode"
    />
    <app-entrance @changeInput="submit" />
  </div>
</template>

<style scoped>
.container {
  display: grid;
  grid-template-rows: 1fr 8fr 1fr;

  background-color: var(--primary);
  width: 100%;
  height: 100%;
  padding: 0.5rem;

  position: relative;
  transition-property: transform;
  transition-timing-function: cubic-bezier(0.4, 0, 0.2, 1);
  transition-duration: 1s;
}

.hidden {
  transform: rotateY(180deg);
  opacity: 0;
  position: absolute;
  z-index: -1;
}

@media (min-width: 640px) {
  .container {
    width: auto;
    height: auto;
    min-width: 300px;
  }
}
</style>
