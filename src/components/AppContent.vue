<script setup>
import ContentTask from './ContentTask.vue'
</script>

<template>
  <div class="content">
    <content-task />
  </div>
</template>

<style scoped>
.content {
  overflow-y: auto;
}

@media (min-width: 640px) {
  .content {
    max-height: 400px;
  }
}
</style>
