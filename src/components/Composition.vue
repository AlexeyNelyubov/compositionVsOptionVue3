<script setup>
import { ref, computed } from "vue";

const task = ref("");
const tasks = ref([]);
const addNewTask = () => {
  tasks.value.push(task.value);
  task.value = "";
};
const deliteTask = (task) => {
  tasks.value.splice(tasks.value.indexOf(task), 1);
};

const numberOfTasks = computed(() => {
  return tasks.value ? tasks.value.length : 0;
});
</script>

<template>
  <main class="composition">
    <h1 class="composition__title">Composition</h1>
    <p class="composition__numer-of-tasks">
      I have {{ numberOfTasks }} tasks today!
    </p>
    <input
      placeholder="Add a new task"
      v-model="task"
      class="composition__add-task-field"
      @keydown.enter="addNewTask"
    />
    <div class="composition__task-list">
      <ul v-for="task in tasks" :key="task.id">
        <div class="composition__task-list-single-task">
          <li>{{ task }}</li>
          <button
            class="composition__task-list-single-task-delite"
            @click="deliteTask(task)"
          >
            x
          </button>
        </div>
      </ul>
    </div>
  </main>
</template>

<style>
.composition {
  display: flex;
  flex-direction: column;
  align-items: center;
}
.composition__title {
  font-size: calc(var(--font-size) + 24px);
}
.composition__numer-of-tasks {
  margin: 5vh;
  font-size: var(--font-size);
}

.composition__add-task-field {
  padding: 1vh 2vw;
  font-size: calc(var(--font-size) - 6px);
}

.composition__task-list {
  width: 50vw;
  margin-top: 3vh;
  font-size: var(--font-size);
}

.composition__task-list-single-task {
  display: flex;
  align-items: flex-end;
  margin-bottom: 2vh;
}

.composition__task-list-single-task-delite {
  background-color: #fff;
  width: var(--font-size);
  height: var(--font-size);
  margin-left: 1vh;
}
</style>
