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
      numberOfPlayableBoxes: 1,
    };
  },
  methods: {
    checkBoxClickedFunc(idArgument, checkedArgument, disabledArgument) {
      //alert(checkedArgument);
      this.testtext = idArgument;
      this.testchecked = checkedArgument;

      let arrayIndex1 = Math.floor(idArgument / this.numberOfRows);
      let arrayIndex2 = idArgument % this.numberOfRows;
      //alert(arrayIndex1 + ' ' + arrayIndex2);

      if (this.checkBoxes[arrayIndex1][arrayIndex2].isChecked === true) {
        this.checkBoxes[arrayIndex1][arrayIndex2].isChecked = false;
        //alert('true');
        this.checkRandomBox(arrayIndex1, arrayIndex2);
      } else {
        //alert('false');
        //this.checkBoxes[arrayIndex1][arrayIndex2].isChecked = true;
        //this.checkBoxes[arrayIndex1][arrayIndex2].isChecked = false;
      }
      //alert(checkedArgument);
    },
    checkRandomBox(arrayIndex1, arrayIndex2) {
      let maxIndex = this.checkBoxes.length;

      let randomId1;
      let randomId2;
      do {
        randomId1 = this.randomInt(maxIndex);
        randomId2 = this.randomInt(maxIndex);
      } while (arrayIndex1 === randomId1 && arrayIndex2 === randomId2); //makes sure new random box is not the same as the last

      this.checkBoxes[randomId1][randomId2].isChecked = true;
      this.randomBoxValue = this.checkBoxes[randomId1][randomId2].isChecked;
      this.randomBoxId = randomId1 * maxIndex + randomId2;
    },
    randomInt(max) {
      return Math.floor(Math.random() * max);
    }, // return random integer
    check(row, collumn) {
      this.checkBoxes[row][collumn].isChecked =
        !this.checkBoxes[row][collumn].isChecked;
    },
    startGame() {
      /*
      let maxIndex = this.checkBoxes.length;
      let randomId1;
      let randomId2;
      let randomBoxArray = [];
      let compareArray = [];
      for (let i = 0; i < this.numberOfPlayableBoxes; i++) {
        randomId1 = this.randomInt(maxIndex);
        randomId2 = this.randomInt(maxIndex);
        compareArray = [randomId1, randomId2];
        while (randomBoxArray.includes(compareArray)) {
          randomId1 = this.randomInt(maxIndex);
          randomId2 = this.randomInt(maxIndex);
          compareArray = [randomId1, randomId2];
        }
        randomBoxArray.push([randomId1, randomId2]);

        this.checkBoxes = randomBoxArray;*/
      alert(
        this.arrayOfArraysIncludesArray(
          [
            [0, 1],
            [1, 0],
          ],
          [0, 1]
        )
      );
    },
    arrayOfArraysIncludesArray(arrayOfArrays, includesArray) {
      for (let i = 0; i < arrayOfArrays.length; i++) {
        JSON.stringify(arrayOfArrays[i]) === JSON.stringify(includesArray);
        //arrayOfArrays.forEach((containedArray) => {
        /*
        if (arrayOfArrays[i].length != includesArray.length) {
          continue;
        }
        for (let j = 0; j < arrayOfArrays[i].length; j++) {
          if (arrayOfArrays[j] != includesArray[j]) {
            return false;
          }
        }
        /*
        if (containedArray == includesArray) {
          return true;
        }*/
      } //);
      return false;
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
          loopArray.push({
            id: checkBoxIndex,
            isChecked: false,
            isDisabled: false,
          });
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
  <br />
  <label for="number_of_rows">Number of rows: </label>
  <input
    id="number_of_rows"
    class="centerInput"
    type="number"
    min="2"
    max="10"
    v-model="numberOfRows"
  />

  <label for="number_of_boxes"> Number of boxes: </label>
  <input
    id="number_of_boxes"
    class="centerInput"
    type="number"
    min="1"
    v-bind:max="
      Math.round(((this.checkBoxes.length * this.checkBoxes.length) / 100) * 40)
    "
    v-model="numberOfPlayableBoxes"
  />
  <br />
  <button id="startGameButton" v-on:click="startGame">Start game!</button>

  <p>numberOfRows: {{ numberOfRows }}</p>
  <p>checkBoxes: {{ checkBoxes }}</p>
  <p>testtext: {{ testtext }}</p>
  <p>testchecked: {{ testchecked }}</p>
  <button v-on:click="check(0, 0)">change [x]</button>

  <table class="gameTable">
    <tr v-for="checkBoxArray in checkBoxes">
      <td v-for="checkBox in checkBoxArray">
        <input
          class="bigCheckbox"
          type="checkbox"
          v-bind:id="checkBox.id"
          v-bind:checked="checkBox.isChecked"
          v-bind:disabled="checkBox.isDisabled"
          v-on:click="
            checkBoxClickedFunc(
              checkBox.id,
              checkBox.isChecked,
              checkBox.isDisabled
            )
          "
        />
      </td>
    </tr>
  </table>
  <!--checkBoxClickedFunc(checkBox.id,
          checkBox.isChecked)-->
  <button v-on:Click="checkRandomBox">RandomBox</button>
  <p>randomBoxId: {{ randomBoxId }}</p>
  <p>randomBoxValue: {{ randomBoxValue }}</p>
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
