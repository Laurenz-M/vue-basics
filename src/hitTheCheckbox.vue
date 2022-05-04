<script>
export default {
  data() {
    return {
      testtext: 'Click checkBox to see values!',
      testchecked: 'Click checkBox to see values!',
      randomBoxId: 'Click button to see values!',
      randomBoxValue: 'Click button to see values!',
      numberOfRows: 3,
      checkBoxes: [],
    };
  },
  methods: {
    checkBoxClickedFunc(idArgument, checkedArgument) {
      //alert(checkedArgument);
      this.testtext = idArgument;
      this.testchecked = checkedArgument;

      let arrayIndex1 = Math.floor(idArgument / this.numberOfRows);
      let arrayIndex2 = idArgument % this.numberOfRows;
      //alert(arrayIndex1 + ' ' + arrayIndex2);

      if (this.checkBoxes[arrayIndex1][arrayIndex2].isChecked === true) {
        this.checkBoxes[arrayIndex1][arrayIndex2].isChecked = false;
        //alert('true');
        this.checkRandomBox();
      } else {
        //alert('false');
        this.checkBoxes[arrayIndex1][arrayIndex2].isChecked = false;
      }
      //alert(checkedArgument);
    },
    checkRandomBox() {
      let maxIndex = this.checkBoxes.length;
      let randomId1 = this.randomInt(maxIndex);
      let randomId2 = this.randomInt(maxIndex);
      this.checkBoxes[randomId1][randomId2].isChecked = true;
      this.randomBoxValue = this.checkBoxes[randomId1][randomId2].isChecked;
      this.randomBoxId = randomId1 * maxIndex + randomId2;
    },
    randomInt(max) {
      return Math.floor(Math.random() * max);
    }, // return random integer
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
  <input
    class="centerInput"
    type="number"
    min="1"
    max="10"
    v-model="numberOfRows"
  />
  <p>numberOfRows: {{ numberOfRows }}</p>
  <!--<p>{{ checkBoxes }}</p>-->
  <p>{{ testtext }}</p>
  <p>{{ testchecked }}</p>

  <table class="gameTable">
    <tr v-for="checkBoxArray in checkBoxes">
      <td v-for="checkBox in checkBoxArray">
        <input
          class="bigCheckbox"
          type="checkBox"
          v-bind:id="checkBox.id"
          v-bind:checked="checkBox.isChecked"
          v-on:Click="checkBoxClickedFunc(checkBox.id, checkBox.isChecked)"
        />
      </td>
    </tr>
  </table>
  <button v-on:Click="checkRandomBox">RandomBox</button>
  <p>{{ randomBoxId }}</p>
  <p>{{ randomBoxValue }}</p>
</template>

<style>
input.bigCheckbox {
  width: 50px;
  height: 50px;
}
.gameTable {
  margin-left: auto;
  margin-right: auto;
}
.centerInput {
  margin: 0 auto;
}
</style>
