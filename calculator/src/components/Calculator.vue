<template>
  <div class="Calculator" tabindex="0" @keyup.prevent="keyPressHandler">

    <span class="Calculator__display" v-text="displayValue"/>

    <div class="Calculator__inputs">

      <div class="Calculator__inputs__main">

        <div class="Calculator__inputs__main__actions">

          <div class="Calculator__inputs__main__inputWrapper">
            <input-button v-text="'AC'" @click="onClearClick"/>
          </div>

          <div class="Calculator__inputs__main__inputWrapper">
            <input-button v-text="'+/-'" @click="onNegateClick"/>
          </div>

          <div class="Calculator__inputs__main__inputWrapper">
           <input-button v-text="'%'" @click="onPercentageClick"/>
          </div>


          <!-- Add the actions +/-, % here -->
        </div>

        <div class="Calculator__inputs__main__numbers">

          <div
            v-for="num in [9, 8, 7, 6, 5, 4, 3, 2, 1, 0]"
            :key="num"
            class="Calculator__inputs__main__inputWrapper">
            <input-button
              variant="light"
              :wide="num === 0"
              v-text="num"
              @click="onNumberClick(num)"/>
          </div>

          <input-button v-text="'.'" @click="onDecimalClick"/>

        </div>

      </div>

      <div class="Calculator__inputs__side">
        <input-button
          v-for="op in ['÷', 'x', '-', '+']"
          :key="op"
          v-text="op"
          variant="orange"
          :highlight="op === operator"
          @click="onOperatorClick(op)"/>

        <input-button variant="orange" v-text="'='" @click="onEqualsClick"/>
      </div>

    </div>

  </div>
</template>

<script>
import InputButton from '@/components/InputButton.vue'

export default {

  components: {
    InputButton
  },

  data() {
    return {
      value: 0,
      decimalClicked: false,
      previousValue: null,
      operator: null,
      isNewNumber: false,
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
      if (this.decimalClicked) return `${this.value}.`;
      return this.value;
    }
  },
  methods: {
    onNumberClick(number) {
      if (this.isNewNumber) this.value = 0;
      this.isNewNumber = false;
      let newString = this.value.toString();
      if (this.decimalClicked) newString += '.';
      newString += number.toString();
      this.value =  parseFloat(newString);
      this.decimalClicked = false;
    },
    onDecimalClick() {
      if (this.value.toString().includes('.')) return;
      this.decimalClicked = true;
    },
    onNegateClick() {
      this.value *= -1;
    },
    onPercentageClick() {
      this.value /= 100;
    },
    onOperatorClick(symbol) {
      this.operator = symbol;
      this.previousValue = this.value;
      this.isNewNumber = true
    },
    onClearClick() {
      this.value = 0;
      this.previousValue = null;
      this.operator = null;
      this.decimalClicked = false;
    },
    onEqualsClick() {
      if (!this.operator) return;
      const operation = this.operators[this.operator];
      this.value = operation(this.previousValue, this.value);
      this.previousValue = null;
      this.operator = null;
      this.isNewNumber = true;
    },
    keyPressHandler(event) {
      if (event.key === 'Backspace') return this.onClearClick();
      if (event.key === ' ') return this.onEqualsClick();
      if (event.key === '.') return this.onDecimalClick();
      if (event.key === '/') return this.onOperatorClick('÷');
      if (event.key === '*') return this.onOperatorClick('x');
      if (Object.keys(this.operators).includes(event.key)) {
        return this.onOperatorClick(event.key);
      }
      if (['0', '1', '2', '3', '4', '5', '6', '7', '8', '9'].includes(event.key)) {
        return this.onNumberClick(parseInt(event.key));
      }
    }
  }
}

</script>

<style lang="scss">

$button-spacing-y: 30px;

.Calculator {
  background: black;
  min-height: 100vh;
  display: flex;
  flex-direction: column;
  width: 50%;
  padding: 0 25%;

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
      &__inputWrapper {
        flex-basis: 33.3333%;
        margin-bottom: $button-spacing-y;
      }

      &__actions {
        display: flex;
        flex-direction: row;
      }

      &__numbers {
        display: flex;
        flex-wrap: wrap;
        justify-content: space-around;
      }
    }

    &__side {
      margin-left: 5%;
      display: flex;
      flex-direction: column;

      button {
        margin-bottom: $button-spacing-y;
      }
    }
  }

}
</style>
