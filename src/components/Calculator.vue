<template>
    <div class="calculator">
        <div class="display br-tl br-tr">{{display || 0}}</div>
        <div @click="clear" class="btn op">{{clearText}}</div>
        <div @click="handleNegative" class="btn op">+/-</div>
        <div @click="handleSquareRoot" class="btn op">√</div>
        <div @click="handleOperator('/')" :class="{active: operator === '/'}" class="btn op">÷</div>
        <div @click="handleOperand('7')" class="btn">7</div>
        <div @click="handleOperand('8')" class="btn">8</div>
        <div @click="handleOperand('9')" class="btn">9</div>
        <div @click="handleOperator('x')" :class="{active: operator === 'x'}" class="btn op">x</div>
        <div @click="handleOperand('4')" class="btn">4</div>
        <div @click="handleOperand('5')" class="btn">5</div>
        <div @click="handleOperand('6')" class="btn">6</div>
        <div @click="handleOperator('-')" :class="{active: operator === '-'}" class="btn op">-</div>
        <div @click="handleOperand('1')" class="btn">1</div>
        <div @click="handleOperand('2')" class="btn">2</div>
        <div @click="handleOperand('3')" class="btn">3</div>
        <div @click="handleOperator('+')" :class="{active: operator === '+'}" class="btn op">+</div>
        <div @click="handleOperand('0')" class="btn zero br-bl">0</div>
        <div @click="handleDecimal" class="btn">.</div>
        <div @click="handleEquals" class="btn op br-br">=</div>
    </div>
</template>

<script>
export default {
    data() {
        return {
            display: '',
            storedValue: null,
            operator: null,
            clearText: 'AC'
        };
    },
    methods: {
        handleNegative() {
            if (this.display.indexOf('-') > -1) {
                this.display.replace('-', '');
            } else {
                if (this.display !== '') {
                    this.display = '-' + this.display;
                }
            }
        },
        handleSquareRoot() {
            this.display = String(Math.sqrt(Number(this.display)));
        },
        handleOperand(value) {
            this.clearText = 'C';
            if (value === '0') {
                if (this.display === '') {
                    return;
                }
            }
            if (this.display === 0) {
                this.display = value;
            } else {
                this.display += value;
            }
        },
        handleDecimal() {
            console.log(this.display);
            if (this.display.indexOf('.') > -1) {
                return;
            }
            if (this.display === '') {
                this.display = '0';
            }
            this.display += '.';
        },
        handleOperator(operator) {
            this.operator = operator;
            this.storedValue = this.display;
            this.display = '';
        },
        handleEquals() {
            if (this.operator && this.storedValue) {
                if (this.operator === '+') {
                    this.display = this.handleAddition();
                } else if (this.operator === '-') {
                    this.display = this.handleSubtract();
                } else if (this.operator === '/') {
                    this.display = this.handleDivision();
                } else if (this.operator === 'x') {
                    this.display = this.handleMultiplication();
                }
                this.storedValue = null;
                this.operator = null;
            }
        },
        handleAddition() {
            return String(Number(this.display) + Number(this.storedValue));
        },
        handleSubtract() {
            return String(Number(this.storedValue) - Number(this.display));
        },
        handleDivision() {
            return String(Number(this.storedValue) / Number(this.display));
        },
        handleMultiplication() {
            return String(Number(this.storedValue) * Number(this.display));
        },
        clear() {
            // if (this.) {

            // }
            if (this.clearText === 'AC' && this.storedValue) {
                this.display = '';
                this.storedValue = null;
                this.operator = null;
                this.clearText = 'C';
            } else if (this.clearText === 'C') {
                this.display = '';
                this.clearText = 'AC'
            }
        }
    }
}
</script>

<style>
.calculator {
    display: grid;
    width: 450px;
    margin: 0 auto;
    grid-template-columns: repeat(4, 1fr);
    grid-auto-rows: minmax(50px, auto);
    border-bottom: 1px solid #888;
    border-left: 1px solid #888;
    border-radius: 10px;
}
.calculator div {
    padding: .7em;
    background: #e2ecc9;
    cursor: pointer;
    font-size: 1.5em;
}
.calculator div.active {
    background: red !important;
}
.calculator div:hover {
    background: #d2dcb9
}
.br-tl { border-top-left-radius: 10px; }
.br-tr { border-top-right-radius: 10px; }
.br-bl { border-bottom-left-radius: 10px; }
.br-br { border-bottom-right-radius: 10px; }
.btn {
    border-top: 1px solid #888;
    border-right: 1px solid #888;
}
.op {
    background: tomato !important;
}
.op:hover {
    background: #ef5337 !important;
}
.zero {
    grid-column: 1/3;
    text-align: left;
    padding-left: 50px !important;
}
.display {
    grid-column: 1/5;
    background: #444 !important;
    color: #fff;
    text-align: right;
    font-size: 2em;
    font-weight: bold;
    padding: .75em .5em !important;
}
</style>
