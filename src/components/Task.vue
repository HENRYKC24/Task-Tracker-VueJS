<template>
  <div
    @dblclick="$emit('toggleReminder', task.id)"
    :class="[task.reminder ? 'reminder' : '', 'task']"
  >
    <h3>
      {{ task.text }}
      <i @click="deleteTask(task.id)" class="fas fa-times" />
    </h3>
    <p>{{ task.day }}</p>
  </div>
</template>

<script>
export default {
  name: "Task",
  props: {
    task: Object,
  },
  methods: {
    deleteTask(id) {
      console.log("id", id);
      this.$emit("delete-task", id);
    },
  },
};
</script>

<style scoped>
.fas {
  color: #f00;
}
.task {
  background: #f4f4f4;
  margin: 5px;
  padding: 10px 20px;
  cursor: pointer;
}

.task.reminder {
  border-left: 5px solid green;
}

.task h3 {
  display: flex;
  align-items: center;
  justify-content: space-between;
}
</style>
