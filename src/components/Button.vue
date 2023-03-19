<template>
  <button @click="onClick()" :style="{backgroundColor: color}" class="btn">{{text}}</button>
</template>

<script>
  export default {
    name: "Button",
    props: {
      text: {
        type: String,
        default: 'Add',
      },
      color: {
        type: String,
        default: 'black',
      }
    },
    methods: {
      onClick() {
        console.log('You clicked on the button');
      }
    }
  }
</script>

<style scoped>

</style>