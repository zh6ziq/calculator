<template>
<!--CALCULATOR BODY -->
<div class="calc">

    <!--CALCULATOR BUTTON -->
    <div class="display">{{result || 0}}</div>

    <b-button class="btn clear" @click="clickClear">C</b-button>
    <b-button class="btn operator" @click="clickPercentage">%</b-button>

    <b-button class="btn" @click="clickAppend(7)">7</b-button>
    <b-button class="btn" @click="clickAppend(8)">8</b-button>
    <b-button class="btn" @click="clickAppend(9)">9</b-button>
    <b-button class="btn operator" @click="clickDivide">/</b-button>

    <b-button class="btn" @click="clickAppend(4)">4</b-button>
    <b-button class="btn" @click="clickAppend(5)">5</b-button>
    <b-button class="btn" @click="clickAppend(6)">6</b-button>
    <b-button class="btn operator" @click="clickMultiply">x</b-button>

    <b-button class="btn" @click="clickAppend(1)">1</b-button>
    <b-button class="btn" @click="clickAppend(2)">2</b-button>
    <b-button class="btn" @click="clickAppend(3)">3</b-button>
    <b-button class="btn operator" @click="clickSubtract">-</b-button>

    <b-button class="btn" @click="clickAppend(0)">0</b-button>
    <b-button class="btn" @click="clickDot">.</b-button>
    <b-button class="btn" @click="clickEqual">=</b-button>
    <b-button class="btn operator" @click="clickAdd">+</b-button>

</div>
</template>

<script>
export default {
    data() {
        return {
            result: '',
            prev: null,
            operator: null,
            operatorClick: false
        }
    },
    methods: {
        // C - button
        clickClear() {
            this.result = '';
        },

        // % - button
        clickPercentage() {
            this.result = parseFloat(this.result) / 100;
        },

        // Int button
        clickAppend(number) {
            if (this.operatorClick) {
                this.result = '';
                this.operatorClick = false;
            }
            this.result = this.result + number;
        },

        // '.' decimal button
        clickDot() {
            if (this.result.indexOf('.') === -1) {
                this.clickAppend('.')
            }
        },

        // '/' divide button
        clickDivide() {
            this.operator = (a, b) => b / a;
            this.setPrev();
        },

        // 'x' multiply button
        clickMultiply() {
            this.operator = (a, b) => a * b;
            this.setPrev();
        },

        // '-' minus button
        clickSubtract() {
            this.operator = (a, b) => b - a;
            this.setPrev();
        },

        // '+' plus button
        clickAdd() {
            this.operator = (a, b) => a + b;
            this.setPrev();
        },

        // '=' equal button
        clickEqual() {
            this.result = this.operator(
                parseFloat(this.result),
                parseFloat(this.prev)
            );
            this.prev = null;
        },

        setPrev() {
            this.prev = this.result;
            this.operatorClick = true;
        }

    },

}
</script>

<style>
* {
    background: rgb(53, 94, 95);
}

.calc {
    width: 350px;
    height: 500px;
    margin: 0 auto;
    font-size: 40px;
    display: grid;
    grid-template-columns: repeat(4, 1fr);
    grid-auto-rows: minmax(auto, auto);
    border: 20px groove goldenrod;
    border-radius: 15px;
}

.display {
    grid-column: 1/5;
    background: black;
    color: white;
    padding: 20px;
    text-align: right;
}

.clear {
    grid-column: 1/4;
}

.btn {
    color: black !important;
    font-size: 20px !important;
    padding: 10px;
    background: linear-gradient(white, lightgrey);
    border: 1px solid navy !important;
    cursor: pointer;
}

.btn:active {
    background: black !important;
    color: white !important;
}

.btn:focus {
    outline: 0;
    box-shadow: none !important;
}

.operator {
    color: rgb(219, 0, 0) !important;
}
</style>
