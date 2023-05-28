<script>
export default {
  props: {
    doneTask: {
      type: String,
      required: false,
    },
  },

  data() {
    return {
      doneTasks: [],
    };
  },

  methods: {
    deliteDoneTask(donetask) {
      this.doneTasks.splice(this.doneTasks.indexOf(donetask), 1);
    },
  },

  computed: {
    numberOfDoneTasks() {
      return this.doneTasks ? this.doneTasks.length : 0;
    },
  },

  watch: {
    doneTask() {
      this.doneTasks.push(this.doneTask);
    },
  },
};
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
