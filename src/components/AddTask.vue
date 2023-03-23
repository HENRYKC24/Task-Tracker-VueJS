<template>
  <form @submit="onSubmit" class="add-form">
    <div class="form-control">
      <label for="">Task</label>
      <input type="text" v-model="text" name="text" placeholder="Add Task" />
    </div>
    <div class="form-control">
      <label for="">Day & Time</label>
      <input
        type="text"
        v-model="day"
        name="day"
        placeholder="Add Day & Time"
      />
    </div>
    <div class="form-control form-control-check">
      <label for="">Set Reminder</label>
      <input type="checkbox" v-model="reminder" name="reminder" />
    </div>
    <input type="submit" value="Save Task" class="btn-block" />
  </form>
</template>

<script>
export default {
  name: "AddTask",
  data() {
    return {
      text: "",
      day: "",
      reminder: false,
    };
  },

  methods: {
    onSubmit(e) {
      e.preventDefault();
      if (!this.text || !this.day) {
        alert("Please add a task and day");
        return;
      }
      const { text, day, reminder } = this;
      this.$emit("add-task", {
        text,
        day,
        reminder,
      });
      this.text = "";
      this.day = "";
      this.reminder = false;
    },
  },
};
</script>

<style scoped>
.add-form {
  margin-bottom: 40px;
}

.form-control {
  margin: 20px 0;
}

.form-control label {
  display: block;
}

.btn-block {
  background: black;
  color: white;
  border: none;
  font-size: 17px;
  height: 40px;
  border-radius: 5px;
}

.btn-block:hover {
  background: #333;
  cursor: pointer;
}

.btn-block:active {
  background: #000;
  transform: translateY(2px);
}

.form-control input {
  width: 100%;
  height: 40px;
  margin: 5px;
  padding: 3px 7px;
  font-size: 17px;
}
.form-control-check {
  display: flex;
  align-items: center;
  justify-content: space-between;
}

.form-control-check label {
  flex: 1;
}

.form-control-check input {
  flex: 2;
  height: 20px;
}
</style>
