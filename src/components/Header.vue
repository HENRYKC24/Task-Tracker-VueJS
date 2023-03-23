<template>
  <header>
    <h1>{{title}}</h1>
    <Button @click="$emit('show-hide-form')" text="Add task" />
  </header>
</template>

<script>
  import Button from './Button';
  export default {
    name: "Header",
    props: {
      title: String,
    },
    components: {
      Button,
    }
  }
</script>

<style scoped>
  header {
    display: flex;
    justify-content: space-between;
    align-items: center;
    margin-bottom: 20px;
  }
</style>
