<template>
  <div class="task">
    <span class="task__priority"></span>
    <div class="task__name">task one</div>
    <div class="task__time">2018/5/8 15:32</div>
    <i class="task__delete fa-solid fa-close"></i>
    <input class="task__checkbox" type="checkbox" />
  </div>
  <!-- <div class="task task--done">
      <span class="task__priority"></span>
      <div class="task__name">task one</div>
      <div class="task__time">2018/5/8 15:32</div>
      <i class="task__delete fa-solid fa-close"></i>
      <input class="task__checkbox" type="checkbox" />
    </div> -->
</template>

<style scoped>
.task {
  background-color: white;
  border-radius: 20px;
  padding: 0.25rem 0.5rem;
  margin: 0.5rem;
  display: grid;
  grid-template-areas:
    'task__priority task__name task__delete task__checkbox'
    'task__priority task__time task__delete task__checkbox';
  grid-template-columns: 1fr 5fr 1fr;
  grid-template-rows: 1fr 1fr;
}

.task.task--done {
  background-color: #5f9ea06a;
  color: white;
}

.task.task--done .task__name {
  text-decoration: line-through;
}

.task.task--done .task__time {
  text-decoration: line-through;
}

.task .task__priority {
  background-color: var(--secondary);
  border-radius: 10px;
  margin: 0.5rem 0.25rem;
  grid-column-start: 1;
  grid-row: 1 / 3;
}

.task .task__name {
  margin: 0 0.25rem;
  grid-column-start: 2;
  grid-row: 1 / 2;
}

.task .task__time {
  margin: 0 0.25rem;
  grid-column-start: 2;
  grid-row: 2 / 3;
}

.task .task__delete {
  cursor: pointer;
  display: flex;
  justify-content: center;
  align-items: center;
  grid-column-start: 3;
  grid-row: 1 / 3;
}

.task .task__checkbox {
  display: flex;
  justify-content: center;
  align-items: center;
  grid-column-start: 4;
  grid-row: 1 / 3;
}
</style>
