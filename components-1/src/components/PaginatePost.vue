<script setup>
defineProps({
    inicio: Number,
    fin: Number,
    cantidadPosts: Number
})

const emit = defineEmits(['prev', 'next'])
</script>

<template>
    <div class="btn-group" role="group" aria-label="Basic example">
        <button type="button" class="btn btn-outline-primary" @click="emit('prev')" :disabled="inicio <= 0">Previous</button>
        <button type="button" class="btn btn-outline-primary" @click="emit('next')" :disabled="fin >= cantidadPosts">Next</button>
    </div>
</template>