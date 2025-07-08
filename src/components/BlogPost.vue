<script setup>
    // defineProps(['title', 'body', 'id', 'colorText'])
    defineProps({
        title: String,
        id: Number,
        colorText: String,
        body: {
            typeof: String,
            default: 'Sin descripcion!'
        }
    })

    const emit = defineEmits(['elegirFavorito']);
</script>

<template>
    <div class="card">
        <div class="card-body">
            <h5 class="card-title" :class="`text-${colorText}`">{{ id }} - {{ title }}</h5>
            <p>{{ body }}</p>
            <button @click="emit('elegirFavorito', title)" class="btn btn-outline-primary">Favorito</button>
        </div>
    </div>
</template>