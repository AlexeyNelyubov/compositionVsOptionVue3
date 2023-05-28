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
</script>

<template>
  <div>
    <p class="task-list__number-of-tasks">
      I have {{ numberOfTasks }} tasks today!
    </p>
    <ul v-for="task in tasks" :key="task.id">
      <div class="task-list__single-task">
        <li style="margin-left: 2.2vw">{{ task }}</li>
        <button
          class="task-list__single-task-delite"
          @click="replaceTaskToDoneTasks(task)"
        >
          ✔
        </button>
        <button class="task-list__single-task-delite" @click="deliteTask(task)">
          x
        </button>
      </div>
    </ul>
  </div>
</template>

<style></style>

//style for component located in parent component Option.vue
