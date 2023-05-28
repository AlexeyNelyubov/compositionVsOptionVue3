<script>
import TasksListOption from "@/components/Option/TasksListOption.vue";
import DoneTasksListOption from "@/components/Option/DoneTasksListOption.vue";

export default {
  components: {
    TasksListOption,
    DoneTasksListOption,
  },

  data() {
    return {
      task: "",
      newTask: "",
      doneTask: "",
    };
  },
  methods: {
    addNewTask() {
      this.newTask = this.task;
      this.task = "";
    },
  },
};
</script>

<template>
  <main class="composition">
    <h1 class="composition__title">Option</h1>
    <input
      placeholder="Add a new task"
      v-model="task"
      class="composition__add-task-field"
      @change="addNewTask"
    />
    <div class="composition__task-list">
      <TasksListOption
        :newTask="newTask"
        @replace-task-to-done-tasks="(newDoneTask) => (doneTask = newDoneTask)"
      />
      <DoneTasksListOption :doneTask="doneTask" style="margin-left: 10vw" />
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

.task-list__number-of-tasks {
  margin: 5vh 0;
  font-size: var(--font-size);
}

.task-list__single-task {
  display: flex;
  align-items: flex-end;
  margin-bottom: 2vh;
}

.task-list__single-task-delite {
  background-color: #fff;
  width: var(--font-size);
  height: var(--font-size);
  margin-left: 1vh;
}
</style>
