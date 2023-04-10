<script setup>
import { RouterLink, RouterView } from 'vue-router'
</script>

<template>
  <nav class="navbar bg-dark">
    <div class="container">
      <RouterLink class="navbar-brand text-white" to="/">
        <img src="@/assets/logo.svg" width="30" height="24">
        PokeAPI
      </RouterLink>
      <div>
        <RouterLink class="btn btn-outline-primary me-2" to="/">Home</RouterLink>
        <RouterLink class="btn btn-outline-primary me-2" to="/about">About</RouterLink>
        <RouterLink class="btn btn-outline-primary me-2" to="/pokemons">Pokemons</RouterLink>
        <RouterLink class="btn btn-outline-primary" to="/favoritos">Favoritos</RouterLink>
      </div>
    </div>
  </nav>

  <div class="container text-center mt-5">
    <RouterView />
  </div>
</template>
