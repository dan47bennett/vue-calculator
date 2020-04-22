<template>
  <div class="Calculator">

    <span class="Calculator__display" v-text="displayValue"/>

    <div class="Calculator__inputs">

      <div class="Calculator__inputs__main">

        <div class="Calculator__inputs__main__actions">
          <input-button v-text="'AC'" @click="onClearClick"/>



          <!-- Add the actions +/-, % here -->
        </div>

        <div class="Calculator__inputs__main__numbers">

          <input-button
            variant="light"
            v-for="num in ['9', '8', '7', '6', '5', '4', '3', '2', '1', '0']"
            :key="num"
            v-text="num"
            @click="onNumberClick(num)"/>

          <input-button v-text="'.'" @click="onDecimalClick"/>

        </div>

      </div>

      <div class="Calculator__inputs__side">
        <input-button variant="orange"
          v-for="operator in ['÷', 'x', '-', '+']"
          :key="operator"
          v-text="operator"
          @click="onOperatorClick(operator)"/>

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
      return parseFloat(this.value);
    }
  },
  methods: {
    onNumberClick(number) {
      if (!this.value) return this.value = number;
      this.value +=  number;
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
      this.value = operation(parseFloat(this.previousValue), parseFloat(this.value));
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
    }

    &__side {
      width: 20%;
    }
  }

}
</style>
