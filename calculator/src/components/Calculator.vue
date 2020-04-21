<template>
  <div class="calculator">
    <div class="display">{{ currentValue || '0' }}</div>
    <button class="number" @click="addToCurrentValue(1)">1</button>
    <button class="number" @click="addToCurrentValue(2)">2</button>
    <button class="number" @click="addToCurrentValue(3)">3</button>
    <button class="number" @click="addToCurrentValue(4)">4</button>
  </div>
</template>

<script>
export default {
  data() {
    return {
      currentValue: ''
    }
  },
  methods: {
    addToCurrentValue(number) {
      let newValue;
      if (this.currentValue === '0') {
        newValue = number
      }
      else {
        newValue = this.currentValue + number
      }
      this.currentValue = newValue
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

  .number {
    background-color:darkgrey;
    color: white
  }
</style>
