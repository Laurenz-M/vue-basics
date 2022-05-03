<script>
export default {
  data() {
    return {
      //testtext:""
      numberOfRows: 3,
      checkBoxes: [],
    };
  },
  methods: {
    checkBoxClickedFunc(checkedArgument) {
      //this.testtext = checkedArgument
    },
  },
  watch: {
    numberOfRows(number) {
      this.checkBoxes = [];
      let returnArray = [];
      let loopArray = [];
      let checkBoxIndex = 0;
      for (let i = 0; i < number; i++) {
        loopArray = [];

        for (let i2 = 0; i2 < number; i2++) {
          loopArray.push({ id: checkBoxIndex, isChecked: false });
          checkBoxIndex++;
        }
        returnArray.push(loopArray);
      }
      this.checkBoxes = returnArray;
    },
  },
};
</script>

<template>
  <input type="number" min="1" max="10" v-model="numberOfRows" />
  <p>numberOfRows: {{ numberOfRows }}</p>
  <!--<p>{{ checkBoxes }}</p>-->
  <!--<p>{{ testtext }}</p>-->

  <table>
    <tr v-for="checkBoxArray in checkBoxes">
      <td v-for="checkBox in checkBoxArray">
        <input
          v-bind:id="checkBox.id"
          v-bind:isChecked="false"
          <!--v-on:Click="checkBoxClickedFunc(isChecked)"
          --
        />
        type="checkBox" />
      </td>
    </tr>
  </table>
</template>

<style></style>
