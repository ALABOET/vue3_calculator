<template>
  <div class="calculator_root">
    <div class="calculator_root__output">
      {{currentInputValue}}
    </div>
    <div class="calculator_root__buttons">
      <button class="cell number" @click="inputValue(number)" v-for="number in numbers" :key="number">{{number}}</button>
      <button class="cell operation" @click="inputOperation(operation)" v-for="operation in operations" :style="{'pointer-events': lastCharIsOperation ? 'none' : 'auto'}" :key="operation">{{operation}}</button>
      <button class="reset" @click="reset">reset</button>
    </div>
  </div>
</template>

<script setup>
import { ref, reactive, computed } from 'vue';
let currentInputValue = ref('0');
let numbers = reactive(['1', '2', '3', '4', '5', '6', '7', '8', '9', '0']);
let operations = reactive(['+', '-', '*', '-', '=']);

const lastCharIsOperation = computed(() => {
  return operations.some((value) => value === currentInputValue.value[currentInputValue.value.length-1])
})

let inputValue = (num) => {
  if (currentInputValue.value === '0') currentInputValue.value = ''
  currentInputValue.value += num
}
let inputOperation = (operation) => {
  if (operation === '=') return currentInputValue.value = eval(currentInputValue.value);
  currentInputValue.value += operation;
}
let reset = () => currentInputValue.value = '0';
</script>

<style lang="scss">
.calculator_root {
  width: 200px;
  input {
    width: 96%;
  }
  &__buttons {
    display: flex;
    flex-wrap: wrap;
    justify-content: space-around;
    width: 100%;
    .number {
      color: white;
      background: darkblue;
    }
    .operation {
      background: orange;
    }
    .reset {
      background: orange;
      width: 100%;
    }
    .cell {
      width: 33%;
    }
  }
}
</style>
