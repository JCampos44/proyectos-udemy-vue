<script setup>
import { useFavoritosStore } from '@/store/favoritos'
import { storeToRefs } from 'pinia';
import { RouterLink } from 'vue-router';

const useFavoritos = useFavoritosStore()

const { favoritos } = storeToRefs(useFavoritos)
const { remove } = useFavoritos

</script>

<template>
    <h1>Favoritos</h1>
    <hr>
    <p v-if="favoritos.length <= 0">Sin favoritos</p>
    <ul class="list-group mt-2" v-else>
        <li class="list-group-item" v-for="poke in favoritos" :key="poke.id">

            <div class="d-flex justify-content-center align-items-center">
                <RouterLink :to="`/pokemons/${poke.name}`">{{ poke.name }}</RouterLink>
                <button class="btn btn-sm btn-danger ms-2" @click="remove(poke.id)">Eliminar</button>
            </div>
        </li>
    </ul>
</template>