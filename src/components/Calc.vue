<template>
  <div>
    <div class="container">
      <button class="display">{{ current }}</button>
      <button class="clear" @click="clear">Ce</button>
      <button class="per" @click="percentage">%</button>
      <button class="change" @click="change">+/-</button>
      <button @click="divide" class="divide operator">÷</button>
      <button @click="number('7')">7</button>
      <button @click="number('8')">8</button>
      <button @click="number('9')">9</button>
      <button @click="times" class="times operator">x</button>
      <button @click="number('4')">4</button>
      <button @click="number('5')">5</button>
      <button @click="number('6')">6</button>
      <button @click="subtract" class="subtract operator">-</button>
      <button @click="number('1')">1</button>
      <button @click="number('2')">2</button>
      <button @click="number('3')">3</button>
      <button @click="add" class="add operator">+</button>
      <button class="zero" @click="number('0')">0</button>
      <button class="decimal" @click="decimalCheck">.</button>
      <button @click="equal" class="equal">=</button>
    </div>
  </div>
</template>

<script>
export default {
  name: "Calc",
  data() {
    return {
      previous: null,
      current: "" || 0,
      selectedOperator: false,
      decimal: false,
      changed: false,
      operator: null
    };
  },
  methods: {
    clear() {
      this.current = "" || 0;
    },
    percentage() {
      this.current = `${this.current / 100}`;
    },
    change() {
      if (this.changed == false) {
        this.current = "-" + this.current;
        this.changed = true;
      } else {
        this.current = this.current.replace("-", "") || this.current.replace();
        this.changed = false;
      }

      if (parseFloat(this.current) < 0) {
        this.current = `${this.current.slice(0)}`;
      }
    },
    number(num) {
      if (this.selectedOperator) {
        this.current = "";
        this.selectedOperator = false;
      }

      if (this.current[0] == "0") {
        this.current = this.current.replace("0", "");
      }
      this.current += num;
    },
    decimalCheck() {
      if (this.current.includes(".")) {
        this.decimal = true;
      } else {
        this.decimal = false;
      }

      if (this.decimal) {
        this.current = "ERROR";
      } else {
        this.current += ".";
      }
    },
    setPrevious() {
      this.previous = this.current;
      this.selectedOperator = true;
    },
    divide() {
      this.operator = (a, b) => a / b;
      this.setPrevious();
    },
    times() {
      this.operator = (a, b) => a * b;
      this.setPrevious();
    },
    subtract() {
      this.operator = (a, b) => a - b;
      this.setPrevious();
    },
    add() {
      this.operator = (a, b) => a + b;
      this.setPrevious();
    },
    equal() {
      this.current = `${this.operator(
        parseFloat(this.previous),
        parseFloat(this.current)
      )}`;
      this.previous = null;
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.container {
  display: grid;
  grid-template-columns: 1fr 1fr 1fr 1fr;
  grid-auto-rows: auto;
  justify-items: center;
  width: 40%;
  margin: 0 auto;
  height: 500px;
}

button {
  background: #fff;
  border: none;
  width: 100%;
  border: solid 1px grey;
  font-size: 30px;
  cursor: pointer;
}

.display {
  grid-column: 1 / span 4;
  background: black;
  opacity: 0.8;
  color: #fff;
}

.zero {
  grid-column: 1 / span 2;
}

.operator {
  opacity: 0.6;
}
</style>
