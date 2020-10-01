<template>
  <div class="calculator">
    <div class="display">{{ current || "0" }}</div>
    <div @click="clear" class="numb">C</div>
    <div @click="sign" class="numb">+/-</div>
    <div @click="mod" class="numb">%</div>
    <div @click="division" class="numb operator">/</div>
    <div @click="process('7')" class="numb">7</div>
    <div @click="process('8')" class="numb">8</div>
    <div @click="process('9')" class="numb">9</div>
    <div @click="multp" class="numb operator">x</div>
    <div @click="process('4')" class="numb">4</div>
    <div @click="process('5')" class="numb">5</div>
    <div @click="process('6')" class="numb">6</div>
    <div @click="minus" class="numb operator">-</div>
    <div @click="process('1')" class="numb">1</div>
    <div @click="process('2')" class="numb">2</div>
    <div @click="process('3')" class="numb">3</div>
    <div @click="plus" class="numb operator">+</div>
    <div @click="process('0')" class="numb zero">0</div>
    <div @click="dot" class="numb">.</div>
    <div @click="equals" class="numb operator">=</div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      previous: null,
      current: " ",
      operator: null,
      operatorClicked: false
    };
  },
  methods: {
    clear() {
      this.current = " ";
    },
    sign() {
      this.current =
        this.current.charAt(0) === "-"
          ? this.current.slice(1)
          : `-${this.current}`;
    },
    mod() {
      this.current = `${parseFloat(this.current) / 100}`;
    },
    process(number) {
      if (this.operatorClicked) {
        this.current = "";
        this.operatorClicked = false;
      }
      this.current = `${this.current}${number}`;
    },
    division() {
      this.operator = (a, b) => a / b;
      this.previous = this.current;
      this.operatorClicked = true;
    },
    multp() {
      this.operator = (a, b) => a * b;
      this.previous = this.current;
      this.operatorClicked = true;
    },
    minus() {
      this.operator = (a, b) => a - b;
      this.previous = this.current;
      this.operatorClicked = true;
    },
    plus() {
      this.operator = (a, b) => a + b;
      this.previous = this.current;
      this.operatorClicked = true;
    },
     dot() {
      if (this.current.indexOf(".") === -1) {
        this.process(".");
      }
    },
    equals() {
      this.current = `${this.operator(
        parseFloat(this.current),
        parseFloat(this.previous)
      )}`;
      this.previous = null;
    },
  },
};
</script>


<style  scoped>
.calculator {
  border-radius: 10px;
  width: 400px;
  margin: 0 auto;
  font-size: 40px;
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  grid-auto-rows: minmax(70px, auto);
  text-align: center;
  background-image: linear-gradient(
    to bottom right,
    rgb(151, 105, 151),
    rgb(0, 255, 149)
  );
}
.display {
  border-radius: 8px;
  margin-bottom: 10px;
  color: aliceblue;
  grid-column: 1/5;
  text-align: right;
}

.numb {
  opacity: 0.6;
  transition: 0.3s;
  padding-top: 10px;
  margin: 4px 5px;
  background-color: #f2f2f2;
  border: 1px solid #999;
  border-radius: 50px;
  align-items: flex-end;
}
.numb:hover {
  opacity: 3;
}
.zero {
  grid-column: 1/3;
  color: #333;
  background-color: lightcyan;
}
.operator {
  color: #333;
  background-color: lightcyan;
}
</style>
