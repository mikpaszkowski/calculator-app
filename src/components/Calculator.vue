<template>
  <div class="calculator-app">
    <div class="result">
      <p class="currentNumber">{{ currData || "0" }}</p>
      <div class="resultNumber">{{ currResult }}</div>
    </div>
    <div class="btn" @click="clearEntry">CE</div>
    <div class="btn" @click="setPercent">%</div>
    <div class="btn" @click="clearAllInputs">C</div>
    <div class="btn" @click="clearLastEntryDigit">
      <ion-icon name="backspace-outline"></ion-icon>
    </div>
    <div @click="oneDevideByX" class="btn">1 &#8725; x</div>
    <div @click="xToPowerOfTwo" class="btn">x&#178;</div>
    <div @click="squareRoot" class="btn">&#8730;x</div>
    <div @click="divide" class="btn">÷</div>
    <div @click="appendDigit('7')" class="digits btn">7</div>
    <div @click="appendDigit('8')" class="digits btn">8</div>
    <div @click="appendDigit('9')" class="digits btn">9</div>
    <div @click="multiply" class="btn">&#215;</div>
    <div @click="appendDigit('4')" class="digits btn">4</div>
    <div @click="appendDigit('5')" class="digits btn">5</div>
    <div @click="appendDigit('6')" class="digits btn">6</div>
    <div @click="subtract" class="btn">-</div>
    <div @click="appendDigit('1')" class="digits btn">1</div>
    <div @click="appendDigit('2')" class="digits btn">2</div>
    <div @click="appendDigit('3')" class="digits btn">3</div>
    <div class="btn" @click="add">+</div>
    <div class="btn" @click="changeSign">+ &#8725; -</div>
    <div @click="appendDigit('0')" class="btn">0</div>
    <div class="btn" @click="insertComma">,</div>
    <div @click="equal" class="btn equal">=</div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      currData: "",
      currResult: "",
      previousInput: null,
      clickedOperation: false,
      operator: null,
      equalClicked: false,
    };
  },
  methods: {
    setPercent() {
      this.currData = `${parseFloat(this.currData) / 100}`;
    },
    clearEntry() {
      this.currData = "";
    },
    clearAllInputs() {
      this.currResult = "";
      this.currData = "";
    },
    clearLastEntryDigit() {
      let temp = this.currData.slice(0, this.currData.length - 1);
      this.currData = temp;
    },
    appendDigit(digit) {
      if (this.clickedOperation) {
        this.currData = "";
        this.clickedOperation = false;
      }
      this.reduceLengthOfNumber(this.currData);
      this.clearResBeforeCalc();
      this.currData = `${this.currData}${digit}`;
    },
    changeSign() {
      this.currData = -this.currData;
    },
    insertComma() {
      if (this.currData.indexOf(",") === -1 && this.currData.length > 0) {
        this.appendDigit(",");
      }
    },
    setOperation() {
      this.previousInput = this.currData;
      console.log("this.previousInput " + this.previousInput);
      console.log("this.currData " + this.currData);
      this.clickedOperation = true;
      this.equalClicked = false;
    },
    oneDevideByX() {
      this.currData = `${1 / this.currData}`;
    },
    xToPowerOfTwo() {
      this.currData = `${Math.pow(this.currData, 2)}`;
    },
    squareRoot() {
      this.currData = `${Math.sqrt(this.currData)}`;
    },
    divide() {
      this.operator = (x, y) => x / y;
      this.currResult = `${this.currData} ÷ `;
      this.setOperation();
    },
    multiply() {
      this.operator = (x, y) => x * y;
      this.currResult = `${this.currData} x `;
      this.setOperation();
    },
    subtract() {
      this.operator = (x, y) => x - y;
      this.currResult = `${this.currData} - `;
      this.setOperation();
    },
    add() {
      this.operator = (x, y) => x + y;
      this.currResult = `${this.currData} + `;
      this.setOperation();
    },
    equal() {
      this.currResult = `${this.currResult}${this.currData} =`;
      this.currData = `${this.operator(
        parseFloat(this.previousInput),
        parseFloat(this.currData)
      )}`;
      this.reduceLengthOfNumber(this.currData);
      this.clickedOperation = true;
      this.equalClicked = true;
    },
    clearResBeforeCalc() {
      if (this.equalClicked) {
        this.currData = "";
        this.currResult = "";
      }
      this.equalClicked = false;
    },
    reduceLengthOfNumber(number) {
      if (number.length > 15) {
        this.currData = parseFloat(number).toExponential(10);
      }
    },
  },
};
</script>

<style lang="scss" scoped>
.calculator-app {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  grid-auto-rows: minmax(50px, auto);
  width: 400px;
  margin: 0 40%;
  padding: 10px;
  font-size: 20px;
  border-radius: 15px;
  color: white;
  box-shadow: 0px 2px 17px 8px #313131;

  .result {
    position: relative;
    grid-column: 1/5;
    display: flex;
    justify-content: center;
    align-items: center;
    height: 150px;
    background-color: #5fc4af;
    border-radius: 15px;
    margin-bottom: 10px;

    .currentNumber {
      position: absolute;
      right: 10px;
      bottom: 2px;
      font-size: 40px;
      margin: 0;
    }
    .resultNumber {
      position: absolute;
      right: 15px;
      top: 15px;
    }
  }
  .btn {
    display: flex;
    justify-content: center;
    align-items: center;
    border: 1px solid rgb(255, 255, 255);
    border-radius: 7px;
    margin: 2px 2px;
    transition: background-color 0.2s;
    cursor: default;

    &:hover {
      background-color: #95d6c9;
    }
  }
  .digits {
    background-color: #175d4e;

    &:active {
      animation: press_button 0.1s ease-in-out;
    }
  }
  .equal {
    background-color: #95d6c9;
  }
}

//animations
@keyframes press_button {
  0% {
    transform: scale(1, 1);
  }
  100% {
    transform: scale(0.9, 0.9);
  }
}
</style>
