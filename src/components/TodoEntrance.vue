<script setup>
defineProps(["todoInput"])
defineEmits(['changeInput','submit'])
</script>

<template>
  <form class="entrance-form" @submit.prevent="$emit('submit', $event)">
    <input name="input" type="text" placeholder="Enter your task" :value="todoInput"  @change="$emit('changeInput', $event)"/>
    <button :disabled="!todoInput" type="submit">
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
  width: 80%;
}

.entrance-form button {
  font-size: 1.5rem;
}
</style>
