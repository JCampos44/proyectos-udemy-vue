<script setup>
import axios from 'axios';
import { ref } from 'vue';
import { useRoute, useRouter } from 'vue-router';

const route = useRoute()
const router = useRouter()

const pokemon = ref({})

const back = () => {
    router.push('/pokemons')
}

const getData = async () => {
    try {
        const { data } = await axios.get(`https://pokeapi.co/api/v2/pokemon/${route.params.name}`)
        console.log(data);
        pokemon.value = data
    } catch (error) {
        console.log(error)
        pokemon.value = null
    }
}

getData()
</script>

<template>
    <div v-if="pokemon">
        <img :src="pokemon.sprites?.front_default" alt="">
        <h1>Pokemon name: {{ $route.params.name }}</h1>
    </div>
    <div v-else>
        <h1>No existe el pokemon</h1>
    </div>
    <button @click="back" class="btn btn-outline-primary">Volver</button>
</template>