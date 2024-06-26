<script setup>
import { ref } from 'vue'
import ChildComponentWithProps from './ChildComponentWithProps.vue'

const greeting = ref('Hello from parent')
</script>

<template>
  <body class="body">
    <ChildComponentWithProps :msg="greeting" />

  </body>
</template>