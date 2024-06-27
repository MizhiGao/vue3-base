<script setup>
import { ref } from 'vue'

const text = ref('')
</script>

<template>
    <div class="body">
        <input v-model="text" placeholder="Type here" class="input">
        <p>{{ text }}</p>
    </div>
</template>

