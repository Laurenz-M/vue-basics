<script>
function newPopup(url) {
  popupWindow = window.open(
    url,
    'popUpWindow',
    'height=300,width=400,left=10,top=10,resizable=yes,scrollbars=yes,toolbar=yes,menubar=no,location=no,directories=no,status=yes'
  );
}

function sleep(delay) {
  let start = new Date().getTime();
  while (new Date().getTime() < start + delay);
}

// Vue Below
export default {
  data() {
    return {
      buttonPressedCount: 0,
      requestedCount: 7,
      tempVar: null,
    };
  },
  methods: {
    increment() {
      this.buttonPressedCount++;
    },
    decrement() {
      this.buttonPressedCount--;
    },
    generateRandom(min, max) {
      if (!max) {
        max = 5;
      } //if is falsy
      if (!min) {
        min = -5;
      }

      this.requestedCount = Math.round(Math.random() * (max - min) + min);
      while (this.requestedCount === 0) {
        this.requestedCount = Math.round(Math.random() * (max - min) + min);
      }
    },
    onInput(e) {
      this.tempVar = e.target.value;
    },
  },
  watch: {
    buttonPressedCount(count) {
      if (count === this.requestedCount) {
        this.buttonPressedCount = 0;
      }
    },
  },
};
</script>

<template>
  <div class="heading">
    <h>The current value is {{ buttonPressedCount }}</h>
    <br />
    <h>The requested value is {{ requestedCount }}</h>
  </div>
  <br />
  <br />
  <div>
    <button class="buttons" v-on:Click="increment">Increment!</button>
    <br />
    <br />
    <button class="buttons" v-on:Click="decrement">Decrement!</button>
    <br />
    <br />

    <!--<button class="buttons" v-on:Click="generateRandom">
      Generate new number!
    </button> -->
  </div>
  <!--<input type="text" v-on:Click="generateRandom" /> -->
  <!-- <input type="text" :value="text" @input="onInput"> -->

  <input v-bind:value="tempVar" @input="onInput" />
  <button class="buttons" @click="generateRandom(tempVar)">
    Generate new number!
  </button>
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
