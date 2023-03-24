<template>
  <div class="container">
    <Header :formHidden="formHidden" @show-hide-form="toggleShowForm" title="Task tracker" />
    <div v-if="!formHidden">
      <AddTask @add-task="addTask" />
    </div>
    <Tasks
      @toggle-reminder="toggleReminder"
      @delete-task="deleteTask"
      :tasks="tasks"
    />
  </div>
</template>

<script>
import Header from "./components/Header";
import Tasks from "./components/Tasks";
import AddTask from "./components/AddTask";

export default {
  name: "App",
  components: {
    Header,
    Tasks,
    AddTask,
  },
  data() {
    return {
      tasks: [],
      formHidden: true,
    };
  },
  methods: {
    deleteTask(id) {
      this.tasks = this.tasks.filter((t) => t.id !== id);
    },
    toggleReminder(id) {
      this.tasks = this.tasks.map((t) => {
        if (t.id === id) {
          return {
            ...t,
            reminder: !t.reminder,
          };
        }
        return t;
      });
    },
    addTask(task) {
      const id = Math.floor(Math.random() * 10000) + 1;
      const newTask = { id, ...task };
      this.tasks = [...this.tasks, newTask];
    },
    toggleShowForm() {
      this.formHidden = !this.formHidden;
    },
  },
  created() {
    this.tasks = [
      {
        id: 1,
        text: "Doctors Appointments",
        day: "March 1 at 2:30pm",
        reminder: true,
      },
      {
        id: 2,
        text: "Meeting at School",
        day: "March 3 at 1:30pm",
        reminder: true,
      },
      {
        id: 3,
        text: "Food Shopping",
        day: "March 3 at 11:00am",
        reminder: false,
      },
    ];
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
