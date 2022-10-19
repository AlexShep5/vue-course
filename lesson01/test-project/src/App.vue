<template>
    <div>
        <input class="inputField" type="number" v-model="operand1">
        <input class="inputField" type="number" v-model="operand2">

        <p>Результат: {{ result }}</p>

        <div>
            <button class="calcBtn" v-on:click="result = Number(operand1) + Number(operand2)">+</button>
            <button class="calcBtn" v-on:click="result = operand1 - operand2">-</button>
            <button class="calcBtn" v-on:click="result = operand1 * operand2">*</button>
            <button class="calcBtn" v-on:click="result = operand1 / operand2">/</button>
        </div>
        <div>
            <button class="calcBtn" v-on:click="result = Math.pow(operand1, operand2)">^</button>
            <button class="calcBtn" v-on:click="result = operand1 % operand2">%</button>
        </div>
    </div>
</template>

<script>
export default {
    name: 'App',
    data() {
        return {
            operand1: 0,
            operand2: 0,
            result: 0
        }
    }
}

</script>

<style lang="scss">
.inputField {
    width: 70px;
    &:not(:first-child) {
        margin-left: 8px;
    }
}
.calcBtn {
    margin: 4px;
    width: 32px;
    height: 32px;
}

</style>
