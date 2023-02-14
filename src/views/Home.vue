<template>
  <div>
    <AddTask v-show="showAddTask" @add-task="addTask" />
    <Task
      v-on:toggle-reminder="toggleReminder"
      v-on:delete-task="deleteTask"
      :tasks="tasks"
    />
  </div>
</template>

<script>
import Task from "../components/Tasks.vue";
import AddTask from "../components/AddTask.vue";

export default {
  name: "HomeComponent",
  props: {
    showAddTask: Boolean,
  },
  components: {
    Task,
    AddTask,
  },
  data() {
    return {
      tasks: [],
    };
  },
  methods: {
    async deleteTask(id) {
      if (confirm("Are you sure?")) {
        const res = await fetch(`api/tasks/${id}`, {
          method: "DELETE",
        });
        res.status === 200
          ? (this.tasks = this.tasks.filter((task) => task.id !== id))
          : alert("Error deleting task");
      }
    },
    async toggleReminder(id) {
      const taskToToggle = await this.fetchTaskData(id);
      const updTask = { ...taskToToggle, reminder: !taskToToggle.reminder };
      const res = await fetch(`api/tasks/${id}`, {
        method: "PUT",
        headers: {
          "Content-type": "application/json",
        },
        body: JSON.stringify(updTask),
      });
      const data = await res.json();
      this.tasks = this.tasks.map((task) =>
        task.id === id ? { ...task, reminder: data.reminder } : task
      );
    },
    async addTask(task) {
      const res = await fetch("/api/tasks", {
        method: "POST",
        headers: {
          "Content-type": "application/json",
        },
        body: JSON.stringify(task),
      });
      const data = await res.json();

      this.tasks = [...this.tasks, data];
    },
    async fetchTasksData() {
      const res = await fetch("api/tasks");
      const data = res.json();
      return data;
    },
    async fetchTaskData(id) {
      const res = await fetch(`api/tasks/${id}`);
      const data = await res.json();
      return data;
    },
  },
  async created() {
    this.tasks = await this.fetchTasksData();
  },
};
</script>