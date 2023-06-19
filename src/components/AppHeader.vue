<template>
  <header>
    <h1>Todo List</h1>
    <nav>
      <button>completed list</button>
      <span>|</span>
      <button>not completed list</button>
    </nav>
  </header>
</template>

<style scoped>
header {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  font-weight: 600;
}

header span {
  color: var(--secondary);
}
</style>
