<template>
  <AddTask v-if="!formHidden" @add-task="addTask" />
  <Tasks
    @toggle-reminder="toggleReminder"
    @delete-task="deleteTask"
    :tasks="tasks"
  />
</template>

<script>
import Header from "../components/Header";
import AddTask from "../components/AddTask";
import Tasks from "../components/Tasks";
import Footer from "../components/Footer";

export default {
  name: "App",
  components: {
    Header,
    AddTask,
    Tasks,
    Footer,
  },
  props: {
    formHidden: Boolean,
  },
  data() {
    return {
      tasks: [],
    };
  },
  methods: {
    async deleteTask(id) {
      const res = await fetch(`api/tasks/${id}`, {
        method: "DELETE",
      });
      res.status === 200
        ? (this.tasks = this.tasks.filter((t) => t.id !== id))
        : alert("Error deleting task");
    },

    async toggleReminder(id) {
      const task = await this.fetchOneTask(id);
      const res = await fetch(`api/tasks/${id}`, {
        method: "PUT",
        headers: {
          "Content-type": "application/json",
        },
        body: JSON.stringify({ ...task, reminder: !task.reminder }),
      });
      res.status === 200
        ? (this.tasks = this.tasks.map((t) => {
            if (t.id === id) {
              return {
                ...t,
                reminder: !t.reminder,
              };
            }
            return t;
          }))
        : alert("Error updating task");
    },

    async addTask(task) {
      const res = await fetch("api/tasks", {
        method: "POST",
        headers: {
          "Content-type": "application/json",
        },
        body: JSON.stringify(task),
      });
      const newTask = await res.json();
      this.tasks = [...this.tasks, newTask];
    },

    async fetchTasks() {
      const res = await fetch("api/tasks");
      const data = await res.json();
      return data;
    },

    async fetchOneTask(id) {
      const res = await fetch(`api/tasks/${id}`);
      const data = await res.json();
      return data;
    },
  },

  async created() {
    this.tasks = await this.fetchTasks();
  },
};
</script>

<style>
@import url("https://fonts.googleapis.com/css2?family=Poppins:wght@300;400&display=swap");
* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}

body {
  font-family: "Poppins", sans-serif;
}

.container {
  max-width: 500px;
  margin: 30px auto;
  overflow: auto;
  min-height: 300px;
  border: 1px solid steelblue;
  padding: 30px;
  border-radius: 5px;
}

.btn {
  display: inline-block;
  background: #000;
  color: #fff;
  border: none;
  padding: 10px 20px;
  margin: 5px;
  border-radius: 5px;
  cursor: pointer;
  text-decoration: none;
  font-size: 15px;
  font-family: inherit;
}

.btn:focus {
  outline: none;
}

.btn-block {
  display: block;
  width: 100%;
}
</style>
