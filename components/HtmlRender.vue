<script setup lang="ts">
import { ref } from 'vue'

const rawHtml = ref('<span style="color:red">Hi!</span>')
</script>

<template>
  <p>Using v-html directive:
    <span v-html="rawHtml"></span>
</p>
</template>