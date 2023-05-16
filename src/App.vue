<template>
    <div class="calculator">
        <div class="screen">{{ display }}</div>
        <div class="button-row">
            <button v-on:click="clear" class="button-grey">AC</button>
            <button v-on:click="sign" class="button-grey">+/-</button>
            <button v-on:click="percent" class="button-grey">%</button>
            <button v-on:click="performOperation('÷')" class="button-orange">÷</button>
        </div>
        <div class="button-row">
            <button v-on:click="inputDigit('7')" class="button-white">7</button>
            <button v-on:click="inputDigit('8')" class="button-white">8</button>
            <button v-on:click="inputDigit('9')" class="button-white">9</button>
            <button v-on:click="performOperation('×')" class="button-orange">×</button>
        </div>
        <div class="button-row">
            <button v-on:click="inputDigit('4')" class="button-white">4</button>
            <button v-on:click="inputDigit('5')" class="button-white">5</button>
            <button v-on:click="inputDigit('6')" class="button-white">6</button>
            <button v-on:click="performOperation('-')" class="button-orange">-</button>
        </div>
        <div class="button-row">
            <button v-on:click="inputDigit('1')" class="button-white">1</button>
            <button v-on:click="inputDigit('2')" class="button-white">2</button>
            <button v-on:click="inputDigit('3')" class="button-white">3</button>
            <button v-on:click="performOperation('+')" class="button-orange">+</button>
        </div>
        <div class="button-row">
            <button v-on:click="inputDigit('0')" class="button-white button-zero">0</button>
            <button v-on:click="inputDecimal" class="button-white">.</button>
            <button v-on:click="calculate" class="button-orange">=</button>
        </div>
    </div>
</template>

<script>
export default {
    data() {
        return {
            display: '0',
            operand1: null,
            operand2: null,
            operator: null,
            decimal: false,
        };
    },
    methods: {
        // Очищує екран та змінні
        clear() {
            this.display = '0';
            this.operand1 = null;
            this.operand2 = null;
            this.operator = null;
            this.decimal = false;
        },
        // Змінює знак числа
        sign() {
            if (this.display !== '0') {
                this.display = parseFloat(this.display) * -1 + '';
            }
        },
        // Відображає відсоткове значення числа
        percent() {
            if (this.display !== '0' && this.operand1 !== null) {
                this.display = (parseFloat(this.operand1) * parseFloat(this.display) / 100) + '';
            }
        },
        // Додає цифру
        inputDigit(digit) {
            if (this.display === '0' || this.display == this.operator) {
                this.display = digit;
            } else {
                this.display += digit;
            }
        },
        // Додає десяткову крапку
        inputDecimal() {
            if (!this.decimal) {
                this.display += '.';
                this.decimal = true;
            }
        },
        // Зберігає введений оператор та перший операнд
        performOperation(operator) {
            this.operator = operator;
            this.operand1 = this.display;
            this.display = operator;
            this.decimal = false;
        },
        // Виконує обчислення
        calculate() {
            this.operand2 = parseFloat(this.display);
            switch (this.operator) {
                case '+':
                    this.display = (parseFloat(this.operand1) + parseFloat(this.operand2)) + '';
                    break;
                case '-':
                    this.display = (parseFloat(this.operand1) - parseFloat(this.operand2)) + '';
                    break;
                case '×':
                    this.display = (parseFloat(this.operand1) * parseFloat(this.operand2)) + '';
                    break;
                case '÷':
                    this.display = (parseFloat(this.operand1) / parseFloat(this.operand2)) + '';
                    break;
                default:
                    break;
            }
            // Очищення для наступних операцiй
            this.operator = null;
            this.operand1 = null;
            this.operand2 = null;
            this.decimal = false;
        },
    },
};
</script>

<style scoped>
.calculator {
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    margin: 0 auto;
    background-color: #f2f2f2;
    border-radius: 20px;
    padding: 20px;
    width: 335px;
}

.screen {
    background-color: #d9d9d9;
    border-radius: 10px;
    color: #000000;
    font-size: 50px;
    font-weight: bold;
    margin-bottom: 20px;
    padding: 20px;
    text-align: right;
    width: 100%;
    overflow: hidden;
}

.button-row {
    display: flex;
    width: 100%;
    gap: 5px;
    padding-bottom: 3px;
}

.button-zero {
    width: 100%;
}

.button-grey {
    background-color: #e0e0e0;
    border-radius: 50%;
    color: #000000;
    font-size: 30px;
    height: 80px;
    min-width: 80px;
}

.button-white {
    background-color: #ffffff;
    border-radius: 50%;
    color: #000000;
    font-size: 30px;
    height: 80px;
    min-width: 80px;
}

.button-orange {
    background-color: #ff9f0a;
    border-radius: 50%;
    color: #ffffff;
    font-size: 30px;
    height: 80px;
    min-width: 80px;
}
</style>