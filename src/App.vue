<script setup>
import AppHeader from './components/AppHeader.vue'
import AppContent from './components/AppContent.vue'
import AppEntrance from './components/AppEntrance.vue'
</script>

<template>
  <div class="container">
    <app-header />
    <app-content />
    <app-entrance />
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
  }
}
</style>
