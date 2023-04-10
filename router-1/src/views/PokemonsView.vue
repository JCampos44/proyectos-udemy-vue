<script setup>
import { RouterLink } from 'vue-router'
import { useGetData } from '@/composables/getData'

const { data, getData, loading, error } = useGetData()

getData('https://pokeapi.co/api/v2/pokemon')
</script>

<template>
    <h1>Pokemons</h1>
    <hr>
    <p v-if="loading">Cargando información...</p>
    <div class="alert alert-danger" v-if="error">
        {{ error }}
    </div>
    <div v-if="data">
        <ul class="list-group">
            <li v-for="(pokemon, index) in data.results" :key="index" class="list-group-item">
                <RouterLink :to="`/pokemons/${pokemon.name}`">
                    {{ pokemon.name }}
                </RouterLink>
            </li>
        </ul>

        <div class="mt-2">
            <button :disabled="!data.previous" class="btn btn-warning me-2"
                @click="getData(data.previous)">Previous</button>
            <button :disabled="!data.next" class="btn btn-primary" @click="getData(data.next)">Next</button>
        </div>


    </div>
</template>