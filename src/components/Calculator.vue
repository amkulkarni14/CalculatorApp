<template>
  <div class = "center">
    <div class="calculator">
      <input
        type="text"
        v-model="display" 
        readonly
        class="display"
      />
      <div class="buttons">
        <button @click="addNumber(7)">7</button>
        <button @click="addNumber(8)">8</button>
        <button @click="addNumber(9)">9</button>
        <button @click="setOperation('/')">/</button>

        <button @click="addNumber(4)">4</button>
        <button @click="addNumber(5)">5</button>
        <button @click="addNumber(6)">6</button>
        <button @click="setOperation('*')">*</button>

        <button @click="addNumber(1)">1</button>
        <button @click="addNumber(2)">2</button>
        <button @click="addNumber(3)">3</button>
        <button @click="setOperation('-')">-</button>

        <button @click="addNumber(0)">0</button>
        <button @click="addDecimal">.</button>
        <button @click="calculateResult">=</button>
        <button @click="setOperation('+')">+</button>

        <button @click="clearDisplay" class="clear">C</button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      display: '',
      currentOperation: null,
      operand1: null,
    };
  },
  methods: {
    addNumber(number) {
      this.display += number;
    },
    addDecimal() {
      if (!this.display.includes('.')) {
        this.display += '.';
      }
    },
    setOperation(operation) {
      if (this.currentOperation) {
        this.calculateResult();
      }
      this.operand1 = parseFloat(this.display);
      this.currentOperation = operation;
      this.display = '';
    },
    calculateResult() {
      if (this.currentOperation) {
        let operand2 = parseFloat(this.display);
        switch (this.currentOperation) {
          case '+':
            this.display = this.operand1 + operand2;
            break;
          case '-':
            this.display = this.operand1 - operand2;
            break;
          case '*':
            this.display = this.operand1 * operand2;
            break;
          case '/':
            this.display = this.operand1 / operand2;
            break;
        }
        this.currentOperation = null;
        this.operand1 = null;
      }
    },
    clearDisplay() {
      this.display = '';
      this.currentOperation = null;
      this.operand1 = null;
    },
  },
};
</script>

<style scoped>
.calculator {
  max-width: 200px;
  margin: 0 auto;
}

.display {
  width: 100%;
  padding: 10px;
  text-align: right;
  font-size: 1.5em;
  border: 1px solid #ddd;
  box-sizing: border-box;
}

.buttons {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  gap: 5px;
}

button {
  padding: 20px;
  font-size: 1.5em;
  border: 1px solid #ddd;
  background-color: #f5f5f5;
}

button:hover {
  background-color: #eee;
}

button.clear {
  grid-column: span 4;
  background-color: #ff9999;
}

button.operator {
  background-color: #f9f9f9;
}
</style>
