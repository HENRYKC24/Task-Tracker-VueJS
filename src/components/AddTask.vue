<template>
  <form class="add-form">
    <div class="form-control">
      <label for="">Task</label>
      <input type="text" name="text" placeholder="Add Task" />
    </div>
    <div class="form-control">
      <label for="">Day & Time</label>
      <input type="text" name="day" placeholder="Add Day & Time" />
    </div>
    <div class="form-control form-control-check">
      <label for="">Set Reminder</label>
      <input type="checkbox" name="reminder" />
    </div>
    <input type="submit" value="Save Task" class="btn-block" />
  </form>
</template>

<script>
export default {
  name: "AddTask",
};
</script>
