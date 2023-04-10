<script setup>
import { onMounted, ref } from 'vue';
import BlogPost from './components/BlogPost.vue'
import PaginatePost from './components/PaginatePost.vue'
import LoadingSpinner from './components/LoadingSpinner.vue'

const posts = ref([])

const favorito = ref('')
const postXpage = 10
const inicio = ref(0)
const fin = ref(postXpage)
const loading = ref(true)

const cambiarFavorito = (title) => {
  favorito.value = title
}

const next = () => {
  inicio.value += postXpage
  fin.value += postXpage
}

const prev = () => {
  inicio.value -= postXpage
  fin.value -= postXpage
}

// onMounted(async () => {
//   try {
//     const res = await fetch('https://jsonplaceholder.typicode.com/posts')
//     posts.value = await res.json()
//   } catch {
//     console.log(error);
//   } finally {
//     loading.value = false
//   }
// })

// fetch('https://jsonplaceholder.typicode.com/posts')
//   .then(res => res.json())
//   .then(data => posts.value = data)
//   .finally(() => {
//     loading.value = false
//   })

const fetchData = async () => {
  try {
    const res = await fetch('https://jsonplaceholder.typicode.com/posts')
    posts.value = await res.json()
  } catch {
    console.log(error);
  } finally {
    loading.value = false
  }
}

fetchData()


</script>

<template>
  <LoadingSpinner v-if="loading" />
  <div class="container" v-else>
    <h1>APP</h1>
    <h2>Mi post favorito: {{ favorito }}</h2>

    <PaginatePost class="mb-2" @prev="prev" @next="next" :inicio="inicio" :fin="fin" :cantidadPosts="posts.length" />

    <BlogPost v-for="post in posts.slice(inicio, fin)" :key="post.id" :title="post.title" :id="post.id" :body="post.body"
      @cambiarFavoritoNombre="cambiarFavorito" class="mb-2"></BlogPost>
  </div>
</template>
