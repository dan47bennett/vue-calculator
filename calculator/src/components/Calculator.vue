<template>
  <div class="calculator">
    <span class="display">{{ currentValue || '0' }}</span>

    <button class="number" @click="appendDigit(7)">7</button>
    <button class="number" @click="appendDigit(8)">8</button>
    <button class="number" @click="appendDigit(9)">9</button>

    <button class="operation" @click="clear">C</button>

    <button class="number" @click="appendDigit(4)">4</button>
    <button class="number" @click="appendDigit(5)">5</button>
    <button class="number" @click="appendDigit(6)">6</button>

    <button class="operation" @click="add">+</button>

    <button class="number" @click="appendDigit(1)">1</button>
    <button class="number" @click="appendDigit(2)">2</button>
    <button class="number" @click="appendDigit(3)">3</button>

    <button class="operation" @click="equals">=</button>


  </div>
</template>

<script>
export default {
  data() {
    return {
      currentValue: '',
      previousValue: '',
      operatorClicked: null,
      operator: null
    }
  },
  methods: {
    appendDigit(number) {
      let newValue;
      if (this.currentValue === '0') {
        newValue = number
      }
      else {
        newValue = this.currentValue + number
      }
      this.currentValue = newValue
    },
    clear() {
      this.currentValue = ''
    },
    operatorSwitch() {
      this.previousValue = this.currentValue;
      this.operatorClicked = true
      this.currentValue = ''
    },
    add() {
      this.operator = (a, b) => a + b;
      this.operatorSwitch();
    },
    equals() {
      this.currentValue = this.operator(
        parseFloat(this.previousValue),
        parseFloat(this.currentValue));
      this.previousValue = ''
    }
  }
}



</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  .calculator {
    display: grid;
    grid-template-columns: repeat(4, 1fr);
  }

  .display {
    grid-column: 1 / 5;
  }

  .operation {
    background-color:orange;
    color: white
  }

  .number {
    background-color:darkgrey;
    color: white
  }
</style>
