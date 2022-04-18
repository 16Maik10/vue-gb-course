<template>
    <div class="wrapper">
        <h3>Калькулятор</h3>
        <label class="keyboard">
            Экранная клавиатура
            <input v-model="showKeyboard" type="checkbox" name="screenKeyboard">
        </label>
        <div v-show="showKeyboard" class="keyboard-btnGroup">
            <button 
            class="keyboard-btn" 
            v-for="(el, i) in keyboard" 
            :key="i" 
            :title="el"
            @click="operands[checked]=operands[checked].concat(el)"
            >{{ el }}</button>
            <button 
            class="keyboard-btn" 
            @click="operands[checked]=operands[checked].slice(0,-1)"
            >&larr;</button>
            <label>
                Первый операнд
                <input type="radio" name="operand" value="first" v-model="checked">
            </label>
            <label>
                Второй операнд
                <input type="radio" name="operand" value="second" v-model="checked">
            </label>
        </div>
        <label>
            Первое число:
            <input v-model.number="operands.first" type="number">
        </label>
        <label>
            Второе число:
            <input v-model.number="operands.second" type="number">
        </label>
        <div class="actions">
            <button @click="result = calculate('+')">Сложение (+)</button>
            <button @click="result = calculate('-')">Вычетание (-)</button>
            <button @click="result = calculate('*')">Умножение (*)</button>
            <button @click="result = calculate('/')" :disabled="!operands.second">Деление (/)</button>
            <button @click="result = calculate('div')" :disabled="!operands.second">Целочисленное деление</button>
            <button @click="result = calculate('exp')">Возведение в степень (x<sup>y</sup>)</button>
        </div>
        <p>Результат: {{ result }}</p>
    </div>
</template>

<script>
export default {
    name: 'appCalc',
    data() {
        return {
            operands: {
                first: '',
                second: ''
            },
            result: null,
            keyboard: ['1', '2', '3', '4', '5', '6', '7', '8', '9', '0'],
            showKeyboard: false,
            checked: 'first',
        }
    },
    methods: {
        sum(first,second) {
            return +first + +second;
        },
        sub(first,second) {
            return first - second;
        },
        multiply(first,second) {
            return first * second;
        },
        div(first,second) {
            return first / second;
        },
        intDiv(first,second) {
            return parseInt(first / second);
        },
        exp(first,second) {
            return first ** second;
        },
        calculate(action){
            const {first,second} = this.operands;
            switch(action){
                case '+': return this.sum(first,second);
                case '-': return this.sub(first,second);
                case '*': return this.multiply(first,second);
                case '/': return this.div(first,second);
                case 'div': return this.intDiv(first,second);
                case 'exp': return this.exp(first,second);
            }
        }
    }
}
</script>

<style scoped>
.wrapper {
    width: fit-content;
    border: 1px solid #000;
    padding: 20px;
}

label {
    display: block;
    margin-bottom: 15px;
}

.keyboard {
    display: flex;
}

.actions {
    display: flex;
    flex-direction: column;
}

button {
    display: block;
    margin-bottom: 10px;
    cursor: pointer;
}


.keyboard-btn {
    display: inline-block;
}

button:disabled {
    cursor: not-allowed;
}
</style>