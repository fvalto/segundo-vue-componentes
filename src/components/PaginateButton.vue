<script setup>
    defineProps({
        inicio: Number,
        fin: Number,
        length: Number
    })

    const emit = defineEmits(['previous', 'next']);
</script>

<template>
    <div class="btn-group" role="group" aria-label="Basic example">
        <button @click="emit('previous')" type="button" class="btn btn-primary" :disabled="inicio <= 0 ? true : false" >Previous</button>
        <button @click="emit('next')" type="button" class="btn btn-primary" :disabled="fin >= length" >Next</button>
    </div>
</template>