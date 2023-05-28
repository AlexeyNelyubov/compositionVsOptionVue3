<script>
export default {
  props: {
    newTask: {
      type: String,
      required: false,
    },
  },

  emits: {
    "replace-task-to-done-tasks": (task) => {
      if (typeof task === "string") {
        return true;
      } else {
        console.warn("Invalid change-time event payload!");
        return false;
      }
    },
  },

  data() {
    return {
      tasks: [],
    };
  },

  methods: {
    deliteTask(task) {
      this.tasks.splice(this.tasks.indexOf(task), 1);
    },
    replaceTaskToDoneTasks(task) {
      this.$emit("replace-task-to-done-tasks", task);
      this.deliteTask(task);
    },
  },

  computed: {
    numberOfTasks() {
      return this.tasks ? this.tasks.length : 0;
    },
  },

  watch: {
    newTask() {
      this.tasks.push(this.newTask);
    },
  },
};
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
