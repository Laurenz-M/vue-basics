<script>
export default {
  data() {
    return {
      buttonPressedCount: 0,
      requestedCount: 7,
    };
  },
  methods: {
    increment() {
      this.buttonPressedCount++;
    },
    decrement() {
      this.buttonPressedCount--;
    },
  },
  watch: {
    buttonPressedCount(count) {
      if (count === this.requestedCount) {
        this.buttonPressedCount = 101;
      }
    },
  },
};
</script>

<template>
  <div class="heading">
    <h>The value is {{ buttonPressedCount }}</h>
  </div>
  <br />
  <br />
  <div>
    <button class="buttons" v-on:Click="increment">Increment!</button>
    <br />
    <br />
    <button class="buttons" v-on:Click="decrement">Decrement!</button>
  </div>
</template>

<style>
.heading {
  text-align: center;
  font-size: 60px;
  font-family: arial;
  font-weight: bold;
}
.buttons {
  background-color: grey;
  color: black;
  width: 180px;
  text-align: center;
  font-size: 30px;
  font-weight: bold;
}
</style>
