<template>
    <div>
        <h1>Calculator</h1>
        <div class="calculator">
            <div class="display">{{ displayValue }}</div>
            <div class="buttons-grid">
                <button @click="handleClick('1')" class="button">1</button>
                <button @click="handleClick('2')" class="button">2</button>
                <button @click="handleClick('3')" class="button">3</button>
                <button @click="handleClick('+')" class="button">+</button>
                <button @click="handleClick('4')" class="button">4</button>
                <button @click="handleClick('5')" class="button">5</button>
                <button @click="handleClick('6')" class="button">6</button>
                <button @click="handleClick('-')" class="button">-</button>
                <button @click="handleClick('7')" class="button">7</button>
                <button @click="handleClick('8')" class="button">8</button>
                <button @click="handleClick('9')" class="button">9</button>
                <button @click="handleClick('*')" class="button">*</button>
                <button @click="handleClick('0')" class="button">0</button>
                <button @click="handleClick('.')" class="button dot">.</button>
                <button @click="handleClick('/')" class="button">/</button>
                <button @click="handleClick('C')" class="clear button">C</button>
                <button @click="handleClick('=')" class="equal button">=</button>
            </div>
        </div>
    </div>
</template>
<script>
export default {
    data() {
        return {
            displayValue: '',
            firstValue: '',
            secondValue: '',
            operator: null,
            waitingForSecondValue: false
        }
    },
    methods: {
        handleClick(value) {
            if (value === 'C') {
                this.displayValue = '';
                this.firstValue = '';
                this.secondValue = '';
                this.operator = null;
                this.waitingForSecondValue = false;
            } else if (value === '=') {
                this.secondValue = this.displayValue;
                this.calculate();
            } else if (['+', '-', '*', '/'].includes(value)) {
                this.waitingForSecondValue = true;
                this.operator = value;
                this.firstValue = this.displayValue;
                this.displayValue = '';
            } else if (value === '.') {
                if (this.displayValue.includes('.')) {
                    return;
                }
                this.displayValue += value;
            } else {
                if (this.waitingForSecondValue) {
                    this.displayValue = '';
                    this.waitingForSecondValue = false;
                }
                this.displayValue += value;
            }
        },
        calculate() {
            if (this.operator === '+') {
                this.displayValue = parseFloat(this.firstValue) + parseFloat(this.secondValue);
            } else if (this.operator === '-') {
                this.displayValue = parseFloat(this.firstValue) - parseFloat(this.secondValue);
            } else if (this.operator === '*') {
                this.displayValue = parseFloat(this.firstValue) * parseFloat(this.secondValue);
            } else if (this.operator === '/') {
                if (this.secondValue === '0') {
                    console.error('Error: Division by zero');
                    return;
                }
                this.displayValue = parseFloat(this.firstValue) / parseFloat(this.secondValue);
            }
            this.firstValue = this.displayValue;
            this.secondValue = '';
            this.operator = null;
        }
    }
}
</script>

<style scoped>
.calculator {
    background-color: #202020;
    width: 300px;
    border-radius: 12px;
    padding: 10px;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    gap: 20px;
}

.display {
    grid-column: span 4;
    height: 50px;
    width: 100%;
    max-width: 100%;
    background-color: #404040;
    color: #fff;
}

.calculator {
    background-color: #202020;
    width: 300px;
    border-radius: 12px;
    padding: 10px;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    gap: 20px;
}

.display {
    grid-column: span 4;
    height: 50px;
    width: 100%;
    max-width: 100%;
    background-color: #404040;
    color: #fff;
    border-radius: 6px;
    display: flex;
    align-items: center;
    justify-content: flex-end;
    font-size: 24px;
}

.buttons-grid {
    display: grid;
    grid-template-columns: repeat(4, 1fr);
    grid-gap: 5px;
    width: 100%;
}

.button {
    height: 45px;
    background-color: #606060;
    color: #fff;
    border-radius: 6px;
    display: flex;
    align-items: center;
    justify-content: center;
    font-size: 20px;
    cursor: pointer;
}

.button:active {
    background-color: #808080;
}

.button.operator {
    background-color: #ff9500;
}

.button.operator:active {
    background-color: #ffac33;
}

.equal {
    grid-column: span 4;
}

.clear {
    background-color: #ff3b30;
}

.button.clear:active {
    background-color: #ff5e3a;
}

h1 {
    color: #fff;
    text-align: center;
}
</style>