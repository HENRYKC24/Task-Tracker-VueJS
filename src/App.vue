<template>
  <div class="container">
    <Header
      :formHidden="formHidden"
      @show-hide-form="toggleShowForm"
      title="Task tracker"
    />
    <!-- <div v-if="!formHidden">
      <AddTask @add-task="addTask" />
    </div> -->
    <router-view :formHidden="formHidden"></router-view>
    <!-- <Tasks
      @toggle-reminder="toggleReminder"
      @delete-task="deleteTask"
      :tasks="tasks"
    /> -->
    <Footer />
  </div>
</template>

<script>
import Header from "./components/Header";
import AddTask from "./components/AddTask";
import Tasks from "./components/Tasks";
import Footer from "./components/Footer";

export default {
  name: "App",
  components: {
    Header,
    AddTask,
    Tasks,
    Footer,
  },
  data() {
    return {
      formHidden: true,
    };
  },
  methods: {
    toggleShowForm() {
      this.formHidden = !this.formHidden;
    },
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
