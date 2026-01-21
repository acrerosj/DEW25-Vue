<script setup>
    import { ref, defineProps } from 'vue'
    const count = ref(0)
    const props = defineProps(['titulo']);
    const emit = defineEmits(['borrarCaracter']);
</script>

<template>
    <span>{{ titulo }}</span>
    <button @click="count++">{{ count }}</button>
    <button @click="$emit('borrarCaracter')">X</button>
</template>

<style scoped>
    button {
        background-color: darksalmon;
    }
    span {
        margin-left: 10px;
        background-color: black;
        color: lightblue;
    }
</style>