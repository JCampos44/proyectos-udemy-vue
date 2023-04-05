<script setup>
import { ref, computed } from 'vue'

const name = 'Vue dinámico'

const counter = ref(0)
const arrayNumeros = ref([])

const increment = () => {
  counter.value++
}

const decrement = () => {
  counter.value--
}

const reset = () => {
  counter.value = 0
}

const addNumero = (numero) => {
  arrayNumeros.value.push(numero)
}

const classCounter = computed(() => {
  if (counter.value == 0) {
    return 'zero'
  }
  if (counter.value > 0) {
    return 'positive'
  }
  if (counter.value < 0) {
    return 'negative'
  }
})

const disableButton = computed(() => {
  return arrayNumeros.value.includes(counter.value)
})

</script>

<template>
  <div class="container text-center mt-3">
    <h1>Hola {{ name.toUpperCase() }}</h1>

    <h2 :class="classCounter">{{ counter }}</h2>

    <div class="btn-group">
      <button @click="increment" class="btn btn-success">Aumentar</button>
      <button @click="decrement" class="btn btn-danger">Disminuir</button>
      <button @click="reset" class="btn btn-secondary">Reset</button>
      <button @click="addNumero(counter)" :disabled="disableButton" class="btn btn-primary">Add</button>
    </div>


    <h2 class="mt-5">Números favoritos</h2>
    <hr>
    <ul v-if="arrayNumeros.length > 0" class="list-group">
      <li v-for="(numero, index) in arrayNumeros" :key="index" class="list-group-item">
        {{ numero }}
      </li>
    </ul>
  </div>
</template>

<style>
h1 {
  color: red;
}

.negative {
  color: red;
}

.positive {
  color: green;
}

.zero {
  color: peru
}
</style>