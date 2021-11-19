/* eslint-disable no-restricted-properties */
<template>
  <div>
    <div>
      <input type="number" v-model.number="op1" />
      <input type="number" v-model.number="op2" />
      = {{ result }}
    </div>
    <!-- <div class="error" v-if="error">Ошибка: {{ error }}</div> -->
    <div>
      <button @click="sum">+</button>
      <button @click="sub">-</button>
      <button @click="div">/</button>
      <button @click="DivInt">/(Int)</button>
      <button @click="mult">*</button>
      <button @click="degree">**</button>
    </div>
  </div>
</template>

<script>
export default {
  name: "Calc",
  data: () => ({
    op1: 0,
    op2: 0,
    result: 0,
    error: "",
  }),
  methods: {
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
    DivInt() {
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
  },
};
</script>
