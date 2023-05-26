<script setup>
import { ref, computed, watch } from "vue";

const props = defineProps({
  newTask: {
    type: String,
    required: false,
  },
});

const emit = defineEmits({
  "replace-task-to-done-tasks": (task) => {
    if (typeof task === "string") {
      return true;
    } else {
      console.warn("Invalid change-time event payload!");
      return false;
    }
  },
});

const tasks = ref([]);

watch(
  () => props.newTask,
  () => {
    tasks.value.push(props.newTask);
  }
);

const deliteTask = (task) => {
  tasks.value.splice(tasks.value.indexOf(task), 1);
};

const replaceTaskToDoneTasks = (task) => {
  emit("replace-task-to-done-tasks", task);
  deliteTask(task);
};

const numberOfTasks = computed(() => {
  return tasks.value ? tasks.value.length : 0;
});

watch(tasks.value, () => {
  console.log("change tasks");
});
</script>

<template>
  <div>
    <p class="composition__numer-of-tasks">
      I have {{ numberOfTasks }} tasks today!
    </p>
    <ul v-for="task in tasks" :key="task.id">
      <div class="composition__task-list-single-task">
        <li style="margin-left: 2.2vw">{{ task }}</li>
        <button
          class="composition__task-list-single-task-delite"
          @click="replaceTaskToDoneTasks(task)"
        >
          ✔
        </button>
        <button
          class="composition__task-list-single-task-delite"
          @click="deliteTask(task)"
        >
          x
        </button>
      </div>
    </ul>
  </div>
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
