<template>
  <div class="entrance">
    <input type="text" placeholder="Enter you task" />
    <button>
      <i class="fa-solid fa-circle-plus"></i>
    </button>
  </div>
</template>

<style scoped>
.entrance {
  display: flex;
  justify-content: center;
  align-items: center;
}

.entrance input {
  border: 2px solid black;
  border-radius: 30px;
  padding: 0.25rem 0.5rem;
  margin: 0.5rem;
  background-color: white;
}

.entrance button {
  font-size: 1.5rem;
}
</style>
