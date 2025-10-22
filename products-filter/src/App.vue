<script setup lang="ts">
import { ref } from 'vue'
const output = ref<string>("0")
const firstNum = ref<number | null>(null)
const operation = ref<string | null>(null)
let isSecondNum = ref<boolean>(false)

function Clear(){
  output.value = "0";
  firstNum.value = null;
  operation.value = null;
  isSecondNum.value = false;
}

function addNumber(number: string){
  if (isSecondNum.value === false){
    if (output.value === "0"){
      output.value = number
    }
    else
    output.value += number
  }

  else {
    if (firstNum !== null && output.value === firstNum.value?.toString()) // Проверка на ввод второго числа
  {
    output.value = number
  }
  else{
    output.value += number
  }
  }
}

function setOperation(operat: string){
  if (firstNum.value === null){
    firstNum.value = parseFloat(output.value)
  }
  else {
    if (operation.value){
      calculate()
    }
  }
  operation.value = operat
  isSecondNum.value = true
  

}

function calculate() {
  if (firstNum.value === null || !operation.value)
    return

    const secondNum = parseFloat(output.value)
    let result = 0

    switch (operation.value){
      case '+': 
        result = firstNum.value + secondNum; 
        break
      case '-':
        result = firstNum.value - secondNum;
        break
      case '*':
        result = firstNum.value * secondNum;
        break
      case '/': 
        result = firstNum.value / secondNum;
        break    
    }
    output.value = result.toString()
    firstNum.value = result
    operation.value = null
    isSecondNum.value = false
}
</script>

<template>
<div class="calc-background">
<span class="brand"> СУПЕР КАЛЬКУЛЯТОР 3 ТЫСЯЧИ</span>
<input class="result-board" v-model="output"/>  
<div class="buttons-grid">
    <button @click="addNumber('1')">1</button>
    <button @click="addNumber('2')">2</button>
    <button @click="addNumber('3')">3</button>

    <button @click="setOperation('+')" class="operation">+</button>

    <button @click="addNumber('4')">4</button>
    <button @click="addNumber('5')">5</button>
    <button @click="addNumber('6')">6</button>

    <button @click="setOperation('-')" class="operation">-</button>

    <button @click="addNumber('7')">7</button>
    <button @click="addNumber('8')">8</button>
    <button @click="addNumber('9')">9</button>

    <button @click="setOperation('*')" class="operation">*</button>

    <button class="clear" @click="Clear">C</button>

    <button @click="addNumber('0')">0</button>

    <button @click="calculate">=</button>

    <button @click="setOperation('/')" class="operation">/</button>

  </div>
</div>
</template>

<style scoped>
  .brand{
    font-size: larger;
    font-weight: bold;
    font-family: inherit;
    display: block;
    align-items: left;
    margin-right: 150px;
    color: lightgray;
  }
  .calc-background{
    
    border: 6px solid rgb(0, 0, 0);
    background-color: rgb(85, 78, 78);
    border-radius: 20px;
    width: 500px;
    height: 600px;
    padding: 10px;
   
  }
  .buttons-grid{
    display: grid;
    grid-template-columns: 1fr 1fr 1fr 1fr;
    gap: 5px;
    row-gap: 20px;
      .clear{
        background-color: rgb(204, 133, 0);
        color: black;
      }

      .operation{
        background-color: white;
        color: black;
      }
  }

  .result-board{
    background-color: aliceblue;
    color: black;
    font-size: large;
    font-weight: bold;
    font-family: inherit;
    border: 8px solid rgb(134, 117, 117);
    border-radius: 25px;
    margin-top: 20px;
    margin-bottom: 60px;
    width: 350px;
    height: 45px;
    
  }
</style>
