<template>
  <div class="Calculator">

    <span class="Calculator__display" v-text="displayValue"/>

    <div class="Calculator__inputs">

      <div class="Calculator__inputs--numbers">
        <button
          v-for="num in [1,2,3,4,5,6,7,8,9,0]"
          :key="num"
          @click="appendDigit(num)"
          v-text="num"/>
        </div>

      <div class="Calculator__inputs--operators">
        <button @click="add">+</button>
        <button @click="clear">C</button>
        <button @click="equals">=</button>
      </div>

    </div>

  </div>
</template>

<script>
export default {
  data() {
    return {
      value: null,
      previousValue: '',
      operatorClicked: null,
      operator: null
    }
  },
  computed: {
    displayValue() {
      if (!this.value) return 0;
      return this.value;
    }
  },
  methods: {
    appendDigit(number) {
      if (!this.value) return this.value = number;
      let valueString = this.value.toString();
      valueString +=  number.toString();
      this.value = parseInt(valueString);
    },
    clear() {
      this.value = null;
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

<style lang="scss">

.Calculator {

  &__display {
    color: green;
  }

  &__inputs {

    &--numbers {
      background-color:darkgrey;
      color: white

    }

    &--operators {
      background-color:orange;
      color: white
    }
  }

}
</style>
