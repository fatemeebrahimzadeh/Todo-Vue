<script setup>
let inputData = ''
defineEmits(['changeInput'])
</script>

<template>
  <form class="entrance-form" @submit.prevent="$emit('changeInput', $event)">
    <input name="input" type="text" placeholder="Enter your task" v-model.trim.lazy="inputData" />
    <button type="submit">
      <i class="fa-solid fa-circle-plus"></i>
    </button>
  </form>
</template>

<style scoped>
.entrance-form {
  display: flex;
  justify-content: center;
  align-items: center;
}

.entrance-form input {
  border: 2px solid black;
  border-radius: 30px;
  padding: 0.25rem 0.5rem;
  margin: 0.5rem;
  background-color: white;
}

.entrance-form button {
  font-size: 1.5rem;
}
</style>
