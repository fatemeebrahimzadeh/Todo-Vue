<script setup>
import { ref } from 'vue'
import TodoHeader from '@/components/TodoHeader.vue'
import TodoList from '@/components/TodoList.vue'
import TodoEntrance from '@/components/TodoEntrance.vue'

const todoInput = ref({})
const todoListMode = ref('')
let countId = 0

function submit(event) {
  const formData = new FormData(event.target)
  const data = {}
  formData.forEach((value, key) => {
    data[key] = value
  })

  if (Object.keys(data).length === 0) {
    console.warn('No form data found')
  }

  if (!data.input) return
  todoInput.value = { task: data.input, taskTime: new Date(), isTaskDone: false, id: countId++ }
  event.target.reset()
}

function changeMode(mode) {
  todoListMode.value = mode
}
</script>

<template>
  <div class="container">
    <todo-header @changeMode="changeMode" />
    <todo-list :todoInput="todoInput" :todoListMode="todoListMode" />
    <todo-entrance @changeInput="submit" />
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
