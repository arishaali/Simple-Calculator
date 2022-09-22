<template>
  <div class="calculator">
    <div class="button display">{{ currentValue || "0" }}</div>
    <div @click="AddNum('1')" class="button">1</div>
    <div @click="AddNum('2')" class="button">2</div>
    <div @click="AddNum('3')" class="button">3</div>
    <div @click="Operation('+')" class="button op">+</div>
    <div @click="AddNum('4')" class="button">4</div>
    <div @click="AddNum('5')" class="button">5</div>
    <div @click="AddNum('6')" class="button">6</div>
    <div @click="Operation('-')" class="button op">-</div>
    <div @click="AddNum('7')" class="button">7</div>
    <div @click="AddNum('8')" class="button">8</div>
    <div @click="AddNum('9')" class="button">9</div>
    <div @click="Operation('*')" class="button op">x</div>

    <div @click="AddNum('0')" class="button zero">0</div>
    <div @click="Operation('.')" class="button op">.</div>
    <div @click="Operation('/')" class="button op">/</div>
    <div @click="clear" class="button clear">C</div>
    <div @click="Operation('-/+')" class="button op">-\+</div>
    <div @click="Operation('%')" class="button op">%</div>
    <div @click="Operation('=')" class="button op">=</div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      currentValue: "",
      previousValue: "",
      operator: null,
    };
  },
  methods: {
    clear() {
      this.currentValue = "";
    },
    AddNum(num) {
      this.currentValue = `${this.currentValue}${num}`;
    },
    Operation(op) {
      if (["/", "*", "-", "+"].includes(op)) {
        this.operator = op;
        this.previousValue = this.currentValue;
        this.currentValue = "";
      }
      if (op === "=") {
        this.currentValue = eval(
          this.previousValue + this.operator + this.currentValue
        );
        this.previousValue = "";
        this.operator = null;
      }
      if (op === "%") {
        this.currentValue = this.currentValue / 100 + "";
      }
      if (op === "-/+") {
        this.currentValue =
          this.currentValue.charAt(0) === "-"
            ? this.currentValue.slice(1)
            : `-${this.currentValue}`;
      }
      if (op === ".") {
        if (this.currentValue === "") {
          this.currentValue = `0${op}`;
        } else {
          this.currentValue = `${this.currentValue}${op}`;
        }
      }
    },
  },
};
</script>

<style scoped>
.calculator {
  background-color: #282828;
  height: 500px;
  width: 300px;
  margin: auto;
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  grid-template-rows: (4, 1fr);
  column-gap: 5px;
  row-gap: 5px;
  padding: 4px;
}
.button {
  background-color: #c05d73;
  color: white;
  font-size: 24px;
  cursor: pointer;
  display: flex;
  justify-content: center;
  align-items: center;
}
.clear{
  background-color: #C184A6;
}
.op {
  background-color: #7E586D;
}
.display {
  grid-column-start: 1;
  grid-column-end: 5;
  background-color: #DCC7D2;
  color: black;
  margin: 4px;
}
.zero {
  grid-column-start: 1;
  grid-column-end: 3;
}
</style>
