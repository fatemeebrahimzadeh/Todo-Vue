<script setup>
import { onMounted, ref, watchEffect } from 'vue'
import AppHeader from '@/components/AppHeader.vue'
import AppContent from '@/components/AppContent.vue'
import AppEntrance from '@/components/AppEntrance.vue'

const inputData = ref([])
const listMode = ref('')

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
  inputData.value.push({ task: data.input, time: new Date(), isChecked: false })
  event.target.reset()
}

function deleteTask(index) {
  inputData.value.splice(index, 1)
}

function checkTask(index) {
  inputData.value[index].isChecked = !inputData.value[index].isChecked
}

function changeMode(mode) {
  listMode.value = mode
}

onMounted(() => {
  const storedData = localStorage.getItem('todoList')
  if (storedData) {
    inputData.value = JSON.parse(storedData)
  }
})

watchEffect(() => {
  localStorage.setItem('todoList', JSON.stringify(inputData.value))
})
</script>

<template>
  <div class="container">
    <app-header @changeMode="changeMode" />
    <app-content
      :inputData="inputData"
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
