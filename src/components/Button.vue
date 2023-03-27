<template>
  <button @click="onClick()" :style="{ backgroundColor: color }" class="btn">
    {{ text }}
  </button>
</template>

<script>
export default {
  name: "Button",
  props: {
    text: String,
    color: String,
    formHidden: Boolean,
  },
  methods: {
    onClick() {
      this.$emit("btn-click");
    },
  },
};
</script>

<style scoped>
button {
  width: 110px;
}
</style>
