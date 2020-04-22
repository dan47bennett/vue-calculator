<template>
  <div class="Calculator">

    <span class="Calculator__display" v-text="displayValue"/>

    <div class="Calculator__inputs">

      <div class="Calculator__inputs__main">

        <div class="Calculator__inputs__main__actions">
          <button v-text="'AC'" @click="onClearClick"/>
          <!-- Add the actions +/-, % here -->
        </div>

        <div class="Calculator__inputs__main__numbers">

          <button
            v-for="num in [9, 8, 7, 6, 5, 4, 3, 2, 1, 0]"
            :key="num"
            v-text="num"
            @click="onNumberClick(num)"/>

          <button v-text="'.'" @click="onDecimalClick"/>

        </div>

      </div>

      <div class="Calculator__inputs__side">
        <button
          v-for="operator in ['÷', 'x', '-', '+']"
          :key="operator"
          v-text="operator"
          @click="onOperatorClick(operator)"/>

        <button v-text="'='" @click="onEqualsClick"/>
      </div>

    </div>

  </div>
</template>

<script>
export default {
  data() {
    return {
      value: null,
      previousValue: null,
      operator: null,
      operators: {
        '÷': (a, b) => a / b,
        'x': (a, b) => a * b,
        '-': (a, b) => a - b,
        '+': (a, b) => a + b
      }
    }
  },
  computed: {
    displayValue() {
      if (!this.value) return 0;
      return this.value;
    }
  },
  methods: {
    onNumberClick(number) {
      if (!this.value) return this.value = number;
      let valueString = this.value.toString();
      valueString +=  number.toString();
      this.value = parseInt(valueString);
    },
    onDecimalClick() {
      alert('not yet implemented init');
    },
    onOperatorClick(symbol) {
      this.operator = symbol;
      this.previousValue = this.value;
      this.value = null;
    },
    onClearClick() {
      this.value = null;
      this.previousValue = null;
      this.operator = null;
    },
    onEqualsClick() {
      const operation = this.operators[this.operator];
      this.value = operation(this.previousValue, this.value);
      this.previousValue = null;
    }
  }
}

</script>

<style lang="scss">

.Calculator {
  background: black;
  min-height: 100vh;
  display: flex;
  flex-direction: column;

  button {
    width: 75px;
    height: 75px;
    font-size: 24px;
    border-radius: 100%;
  }

  &__display {
    color: white;
    font-size: 2rem;
    padding: 2rem;
    font-size: 64px;
    width: 100%;
  }

  &__inputs {
    width: 100%;
    display: flex;
    flex-direction: row;

    &__main {
      width: 80%;

      &__actions {
        button {
          background-color:lightgrey;
          color: black
        }
      }

      &__numbers {
        button {
          background-color:darkgrey;
          color: white
        }
      }

    }

    &__side {
      width: 20%;

      button {
        background-color:orange;
        color: white;
      }
    }
  }

}
</style>
