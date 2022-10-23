<template>
    <div>
        <div class="inputWrap">
            <input class="inputField" type="number" v-model.number="operand1">
            <input class="inputField" type="number" v-model.number="operand2"> = {{ result }}
        </div>
        <div class="calcError" v-show="error">Ошибка! {{ error }}</div>

        <div class="calcWrap">
            <button class="calcBtn" v-for="operand, index in operands" :key="index" @click="calculate(operand)">{{ operand }}</button>
        </div>
        <div>
            <label>
                <p><input type="checkbox" v-model="isKeyboard">Отобразить экранную клавиатуру</p>
            </label>
        </div>
        <div class="keyboard" v-show="isKeyboard">
            <button class="keyBtn" v-for="key, index in keys" :key="index" @click="print(key)">{{ key }}</button>
            <div class="operands">
                <label><input type="radio" name="keyboard" @click="setInput(0)" checked>Операнд 1</label>
                <label><input type="radio" name="keyboard" @click="setInput(1)">Операнд 2</label>
            </div>

        </div>
    </div>
</template>

<script>
export default {
    name: 'App',
    data() {
        return {
            activeInput: 0,
            operand1: 0,
            operand2: 0,
            result: 0,
            error: '',
            operands: ['+', '-', '/', '*', '^', '%'],
            keys: ['0', '1', '2', '3', '4', '5', '6', '7', '8', '9', '\u2190'],
            isKeyboard: false
        }
    },
    methods: {
        add() {
            this.result = this.operand1 + this.operand2
        },
        sub() {
            this.result = this.operand1 - this.operand2
        },
        mult() {
            this.result = this.operand1 * this.operand2
        },
        div() {
            if (this.operand2 == 0) {
                this.error = 'Делить на 0 нельзя!'
            } else {
                this.result = this.operand1 / this.operand2
            }
        },
        pow() {
            this.result = Math.pow(this.operand1, this.operand2)
        },
        remDiv() {
            this.result = this.operand1 % this.operand2
        },
        calculate (operation = '+') {
            this.error = ''
            switch (operation) {
                case '+':
                    this.add()
                    break
                case '-':
                    this.sub()
                    break
                case '*':
                    this.mult()
                    break
                case '/':
                    this.div()
                    break
                case '^':
                    this.pow()
                    break
                case '%':
                    this.remDiv()
                    break
            }
        },
        print (key) {
            if (this.activeInput == 0) {
                const str = String(this.operand1)

                if (key == "\u2190") {
                    this.operand1 = Number(str.slice(0, str.length - 1))
                    return
                }
                this.operand1 = Number(this.operand1 + key);

            } else {
                const str = String(this.operand2)
                if (key == "\u2190") {
                    this.operand2 = Number(str.slice(0, str.length - 1))
                    return
                }
                this.operand2 = Number(this.operand2 + key);
            }
        },

        setInput(inp) {
            if (inp == 0) {
                this.activeInput = 0;
            } else {
                this.activeInput = 1;
            }
        }
    },
}

</script>

<style lang="scss">
.inputWrap {
    margin-top: 16px;

    .inputField {
        width: 90px;
        &:not(:first-child) {
            margin-left: 8px;
        }
    }
}

.calcWrap {
    margin-top: 16px;

    .calcBtn {
        &:not(:first-child) {
            margin-left: 8px;
        }
        width: 32px;
        height: 32px;
    }
}

.calcError {
    margin-top: 8px;
    color: red;
}

.keyBtn {
    &:not(:first-child) {
        margin-left: 8px;
    }
    width: 32px;
    height: 32px;
}

.operands {
    margin-top: 8px;
}

</style>
