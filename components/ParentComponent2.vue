<script setup>
import { ref, reactive } from 'vue'
import ChildComponentWithSlot from './ChildComponentWithSlot.vue'

const msg = ref('from parent')
</script>

<template>
  <body class="body">
    <ChildComponentWithSlot></ChildComponentWithSlot>

  </body>
</template>