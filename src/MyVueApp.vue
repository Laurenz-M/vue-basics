<script>
export default {
  data() {
    return {
      buttonPressedCount: 0,
    };
  },
  methods: {
    increment() {
      this.buttonPressedCount++;
    },
  },
};
</script>

<template>
  <h>You clicked the Button below {{ buttonPressedCount }} times! </h>
  <button v-on:Click="increment">Click me!</button>
</template>

<style></style>
