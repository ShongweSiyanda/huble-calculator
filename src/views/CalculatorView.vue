<template>
  <div>
    <div class="container px-lg-5 py-lg-5 py-4">
      <div class="row">
        <div class="col-sm-2 hide-mobile">&nbsp;</div>
        <div class="col-sm-8">
          <div class="holder py-3 px-3">
            <div class="row">
              <div class="col-12 py-3 px-lg-4 text-center">
                <div class="input py-3 px-lg-5">
                  <form name="calc" id="calc-form">
                    <input type="text" v-model="calculator.inputString"
                           @input="calculator.result = calculation(calculator.inputString)"
                           @keyup="calculator.inputString = disableAlphabets(calculator.inputString)"
                           placeholder="Enter your expression">
                  </form>
                  <div class="math-buttons px-lg-5 mt-3">
                    <div class="row">
                      <div class="col-lg-12 col-12">
                        <calculator-math-button
                            v-for="(operator,i) in mathOperators" :key="i"
                            :operator="operator.sign"
                            @click="addMathOperator(operator.sign)"/>
                      </div>
                    </div>
                  </div>
                </div>
              </div>
              <div class="col-12 py-3 px-lg-4 text-center">
                <div class="output py-3">
                  <div class="row">
                    <div class="col-12"><h3 class="fw-bold">{{ calculator.result }}</h3></div>
                    <div class="col-12"><h3 class="fw-bold">Result : {{ calculator.result }}</h3></div>
                  </div>
                </div>
              </div>
            </div>
          </div>
        </div>
        <div class="col-sm-2 hide-mobile">&nbsp;</div>
      </div>
    </div>
  </div>
</template>
<script setup>

import {reactive} from "vue";
import CalculatorMathButton from '../components/Calculator/MathButton/index.vue'
import {evaluate} from 'mathjs';

const calculator = reactive({
  result: 0,
  inputString: '',
})

const addMathOperator = (operator) => {
  calculator.inputString += `${operator}`
}

const calculation = (input) => {

  if (input !== '') {
    //exclude letter e as it is a mathematical constant
    if (input !== 'e' && input !== 'E') {
      try {
        const result = evaluate(input)
        if (isNumber(result)) {
          return result
        }
      } catch (error) {
        console.log('Math error:' + error)
      }
    }
  }
  return 0
}
const disableAlphabets = (input) => {
  return input.replace(/[^0-9+\-*/.()%]/g, '')
}
const isNumber = (value) => {
  return typeof value === 'number'
}

const mathOperators = [
  {label: 'addition', sign: '+'},
  {label: 'subtraction', sign: '-'},
  {label: 'multiplication', sign: '*'},
  {label: 'division', sign: '/'},
]

</script>
<style scoped>
.holder {
  border: 2px solid #000000;
  border-top: 2rem solid #003562;
}

.input, .output {
  border: 1px solid #003562;
  border-radius: 8px;
}

.input input {
  border: 2px solid #003562;
  border-radius: 6px;
  padding: 13px 20px;
}

.output h3 {
  color: #003562;
}
</style>