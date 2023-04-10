<script setup>
import { ref } from 'vue'
import axios from 'axios'
import { RouterLink } from 'vue-router'

const pokemons = ref([])

const getData = async () => {
    try {
        const { data } = await axios.get('https://pokeapi.co/api/v2/pokemon')
        pokemons.value = data.results
    } catch (error) {
        console.log(error);
    }
}

getData()
</script>

<template>
    <h1>Pokemons</h1>
    <hr>
    <ul>
        <li v-for="(pokemon, index) in pokemons" :key="index">
            <RouterLink :to="`/pokemons/${pokemon.name}`">
                {{ pokemon.name }}
            </RouterLink>
        </li>
    </ul>
</template>