<script setup>
import { ref, computed, watch } from "vue";

const props = defineProps({
  doneTask: {
    type: String,
    required: false,
  },
});

const doneTasks = ref([]);

watch(
  () => props.doneTask,
  () => {
    doneTasks.value.push(props.doneTask);
  }
);

const deliteDoneTask = (donetask) => {
  doneTasks.value.splice(doneTasks.value.indexOf(donetask), 1);
};

const numberOfDoneTasks = computed(() => {
  return doneTasks.value ? doneTasks.value.length : 0;
});
</script>

<template>
  <div>
    <p class="task-list__number-of-tasks">
      I've done {{ numberOfDoneTasks }} tasks today!
    </p>
    <ul v-for="doneTask in doneTasks" :key="doneTask.id">
      <div class="task-list__single-task">
        <li style="margin-left: 2.2vw">{{ doneTask }}</li>
        <button
          class="task-list__single-task-delite"
          @click="deliteDoneTask(doneTask)"
        >
          x
        </button>
      </div>
    </ul>
  </div>
</template>

<style></style>
//style for component located in parent component Option.vue
