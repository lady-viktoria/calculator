/* eslint-disable default-case */
/* eslint-disable no-restricted-properties */
<template>
  <div>
    <div>
      <input
        type="number"
        placeholder="operand1"
        v-model.number="op1"
        @focus="operandRadioChange(1)"
      />
      <input
        type="number"
        placeholder="operand2"
        v-model.number="op2"
        @focus="operandRadioChange(2)"
      />
      = {{ result }}
    </div>
    <!-- <div class="error" v-if="error">Ошибка: {{ error }}</div> -->
    <input type="checkbox" id="checkbox" v-model="keybord" />
    <label for="checkbox">Отобразить экранную клавиатуру</label>
    <br />

    <div class="collection" v-if="keybord">
      <button
        v-for="(item, idx) in collection"
        :key="idx"
        @click="operandChoise(item)"
      >
        {{ item }}
      </button>
      <button @click="deleteLastSymbol()">"Back"</button>
      <!-- {{ collection }} -->
    </div>

    <input type="radio" id="one" value="1" v-model.number="operandRadio" />
    <label for="one">Операнд 1</label>
    <br />
    <input type="radio" id="two" value="2" v-model.number="operandRadio" />
    <label for="two">Операнд 2</label>
    <br />
    <span>Выбрано: {{ operandRadio }}</span>

    <div>
      <button
        v-for="operator of operators"
        @click="calculate(operator)"
        :key="operator"
      >
        {{ operator }}
      </button>
      <!-- <button @click="calculate('-')">-</button>
      <button @click="calculate('/')">/</button>
      <button @click="calculate('/(Int)')">/(Int)</button>
      <button @click="calculate('*')">*</button>
      <button @click="calculate('**')">**</button> -->
    </div>
  </div>
</template>

<script>
export default {
  name: "Calc",
  data: () => ({
    keybord: true,
    operandRadio: 1,
    op1: 0,
    op2: 0,
    result: 0,
    error: "",
    operators: ["+", "-", "/", "/(Int)", "*", "**"],
    collection: [1, 2, 3, 4, 5, 6, 7, 8, 9, 0],
  }),
  methods: {
    operandRadioChange(n) {
      this.operandRadio = n;
    },
    operandChoise(item) {
      // eslint-disable-next-line default-case
      switch (this.operandRadio) {
        case 1:
          this.op1 = +`${this.op1}${item}`;
          break;
        case 2:
          this.op2 = +`${this.op2}${item}`;
          break;
      }
    },
    deleteLastSymbol() {
      // eslint-disable-next-line default-case
      switch (this.operandRadio) {
        case 1:
          this.op1 = Math.floor(this.op1 / 10);
          break;
        case 2:
          this.op2 = Math.floor(this.op2 / 10);
          break;
      }
    },
    sum() {
      this.result = this.op1 + this.op2;
    },
    sub() {
      this.result = this.op1 - this.op2;
    },
    div() {
      const { op1, op2 } = this;
      if (op2 === 0) {
        this.error = "на 0 делить нельзя!";
        this.result = `Ошибка: ${this.error}`;
      } else {
        // т.к. исп деструктуризация, можно исп просто op1, op2
        this.result = op1 / op2;
      }
    },
    divInt() {
      const { op1, op2 } = this;
      if (op2 === 0) {
        this.error = "на 0 делить нельзя!";
        this.result = `Ошибка: ${this.error}`;
      } else {
        // т.к. исп деструктуризация, можно исп просто op1, op2
        this.result = Math.trunc(op1 / op2);
      }
    },
    mult() {
      this.result = this.op1 * this.op2;
    },
    degree() {
      // eslint-disable-next-line no-restricted-properties
      this.result = Math.pow(this.op1, this.op2);
    },
    calculate(operation = "+") {
      // eslint-disable-next-line default-case
      switch (operation) {
        case "+":
          this.sum();
          break;
        case "-":
          this.sub();
          break;
        case "/":
          this.div();
          break;
        case "/(Int)":
          this.divInt();
          break;
        case "*":
          this.mult();
          break;
        case "**":
          this.degree();
          break;
      }
    },
  },
};
</script>
