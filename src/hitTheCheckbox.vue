<script>
export default {
  data() {
    return {
      testtext: '',
      numberOfRows: 3,
      checkBoxes: [],
    };
  },
  methods: {},
  watch: {
    numberOfRows(number) {
      this.checkBoxes = [];
      for (let i = 0; i < number * number; i++) {
        this.checkBoxes.push({ id: i, isChecked: false });
      }
      this.testtext = this.checkBoxes.length;
    },
  },
};
</script>

<template>
  <input type="number" min="1" max="10" v-model="numberOfRows" />
  <p>numberOfRows: {{ numberOfRows }}</p>
  <p>array length: {{ testtext }}</p>
  <!--<p>{{ checkBoxes }}</p>-->

  <table v-for="checkBox in checkBoxes">
    <tr>
      <td><input type="checkBox" /></td>
    </tr>
  </table>
</template>

<style></style>
