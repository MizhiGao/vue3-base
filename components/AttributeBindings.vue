<script setup>
import { ref } from 'vue'

const titleClass = ref('title-red')
</script>

<template>
  <body class="body">
    <h1 :class="titleClass">Make me red</h1>

  </body>
</template>

<style>
.title-red {color: red; }
.title-blue {color: blue; }
</style>