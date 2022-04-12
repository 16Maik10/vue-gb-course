<template>
    <div class="wrapper">
        <h3>Калькулятор</h3>
        <label>
            Первое число:
            <input v-model.number="operand1" type="number">
        </label>
        <label>
            Второе число:
            <input v-model.number="operand2" type="number">
        </label>
        <div class="actions">
            <button @click="result=sum">Сложение (+)</button>
            <button @click="result=sub">Вычетание (-)</button>
            <button @click="result=multiply">Умножение (*)</button>
            <button @click="result=div" :disabled="!operand2">Деление (/)</button>
            <button @click="result=intDiv" :disabled="!operand2">Целочисленное деление</button>
            <button @click="result=exp">Возведение в степень (x<sup>y</sup>)</button>
        </div>

        <p>Результат: {{result}}</p>
    </div>
</template>

<script>
export default {
    name: 'appCalc',
    data(){
        return {
            operand1: null,
            operand2: null,
            result: null,
        }
    },
    computed:{
        sum(){
            return this.operand1 + this.operand2;
        },
        sub(){
            return this.operand1 - this.operand2;
        },
        multiply(){
            return this.operand1 * this.operand2;
        },
        div(){
            return this.operand1 / this.operand2;
        },
        intDiv(){
            return parseInt(this.operand1 / this.operand2);
        },
        exp(){
            return this.operand1 ** this.operand2;
        },
    }
}
</script>

<style scoped>
.wrapper{
    width: fit-content;
    border: 1px solid #000;
    padding: 20px;
}

label{
    display: block;
    margin-bottom: 15px;
}
.actions{
    display: flex;
    flex-direction: column;
}
button{
    display: block;
    margin-bottom: 10px;
    cursor: pointer;
}

button:disabled{
    cursor:not-allowed;
}
</style>