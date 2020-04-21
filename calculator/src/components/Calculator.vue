<template>
  <div class="calculator">
    <div class="display">{{ currentValue }}</div>
    <button class="number">1</button>
    <button class="number">2</button>
    <button class="number">3</button>
    <button class="number">4</button>
  </div>
</template>

<script>
export default {
  data() {
    return {
      currentValue: '123'
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
