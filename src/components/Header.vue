<template>
  <header>
    <h1>{{ title }}</h1>
    <Button
      v-show="shouldShowButton"
      @btn-click="$emit('show-hide-form')"
      :text="formHidden ? 'Add Task' : 'Close'"
      :formHidden="formHidden"
      :color="formHidden ? 'green' : 'red'"
    />
  </header>
</template>

<script>
import Button from "./Button";
export default {
  name: "Header",
  props: {
    title: String,
    formHidden: Boolean,
  },
  components: {
    Button,
  },
  computed: {
    shouldShowButton() {
      return this.$route.path === "/";
    },
  },
};
</script>

<style scoped>
header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 20px;
}
</style>
