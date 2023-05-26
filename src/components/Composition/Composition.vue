<script setup>
import { ref, computed, watch } from "vue";

import TaskList from "@/components/Composition/TasksList.vue";

const task = ref("");
const newTask = ref("");
const doneTask = ref("");

const doneTasks = ref([]);

const addNewTask = () => {
  newTask.value = task.value;
  task.value = "";
};

const deliteDoneTask = (donetask) => {
  doneTasks.value.splice(doneTasks.value.indexOf(donetask), 1);
};

const numberOfDoneTasks = computed(() => {
  return doneTasks.value ? doneTasks.value.length : 0;
});
</script>

<template>
  <main class="composition">
    <h1 class="composition__title">Composition</h1>
    <input
      placeholder="Add a new task"
      v-model="task"
      class="composition__add-task-field"
      @keydown.enter="addNewTask"
    />
    <div class="composition__task-list">
      <TaskList
        :newTask="newTask"
        @replace-task-to-done-tasks="
          (newDoneTask) => (
            (doneTask = newDoneTask), doneTasks.push(newDoneTask)
          )
        "
      />
      <div style="margin-left: 10vh">
        <p class="composition__numer-of-tasks">
          I've done {{ numberOfDoneTasks }} tasks today!
        </p>
        <ul v-for="doneTask in doneTasks" :key="doneTask.id">
          <div class="composition__task-list-single-task">
            <li style="margin-left: 2.2vw">{{ doneTask }}</li>
            <button
              class="composition__task-list-single-task-delite"
              @click="deliteDoneTask(doneTask)"
            >
              x
            </button>
          </div>
        </ul>
      </div>
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

.composition__add-task-field {
  margin-top: 3vh;
  padding: 1vh 2vw;
  font-size: calc(var(--font-size) - 6px);
}

.composition__task-list {
  width: 80vw;
  margin-top: 3vh;
  display: flex;
  justify-content: center;
  font-size: var(--font-size);
}

.composition__numer-of-tasks {
  margin: 5vh 0;
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
