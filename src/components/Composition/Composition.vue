<script setup>
import { ref } from "vue";

import TaskList from "@/components/Composition/TasksList.vue";
import DoneTaskList from "@/components/Composition/DoneTaskList.vue";

const task = ref("");
const newTask = ref("");
const doneTask = ref("");

const addNewTask = () => {
  newTask.value = task.value;
  task.value = "";
};
</script>

<template>
  <main class="composition">
    <h1 class="composition__title">Composition</h1>
    <input
      placeholder="Add a new task"
      v-model="task"
      class="composition__add-task-field"
      @change="addNewTask"
    />
    <!-- @keydown.enter="addNewTask" -->
    <div class="composition__task-list">
      <TaskList
        :newTask="newTask"
        @replace-task-to-done-tasks="(newDoneTask) => (doneTask = newDoneTask)"
      />
      <DoneTaskList :doneTask="doneTask" style="margin-left: 10vw" />
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
</style>
