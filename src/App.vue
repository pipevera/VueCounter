<template>
  <div class="container">
    <h1>contador</h1>
    <h2 :class="classCounter">{{ counter }}</h2>
    <div class="botones">
      <button @click="aumentar">+</button>
      <button @click="disminuir">-</button>
      <button @click="reset">reset</button>
      <button @click="add" :disabled="bloquear">add</button>
    </div>
    
    <h2>contador de clicks: {{ contadorClicks }} </h2>
    <ul>
      <li v-for="(numeros, index) in arrayFavoritos" :key="index">
        {{ numeros }}
      </li>
    </ul>
  </div>
</template>

<script setup>
import {ref, computed} from 'vue'
const counter = ref(0)
const contadorClicks = ref(0)
const arrayFavoritos = ref([])

const bloquear = computed (() => {
  if (arrayFavoritos.value.includes(counter.value)) {
    return true
  }
  
})

const add = () => {
  arrayFavoritos.value.push(counter.value)
}

const aumentar = () => {
  counter.value++;
  contadorClicks.value++;
}

const disminuir = () => {
  counter.value--;
  contadorClicks.value++;
}

const reset = () => {
  counter.value = 0;
  contadorClicks.value == 0;
}

const classCounter = computed (() => {
  if (counter.value === 0) {
    return 'zero'
  }
  if (counter.value > 0) {
    return 'positive'
  } else {
    return 'negative'
  }
})


</script>

<style>
.container {
  width: 100%;
  height: 100vh;
}

.positive {
  color: green;
}

.negative {
  color: red;
}
.zero {
  color: black;
}


</style>