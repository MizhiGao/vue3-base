<script setup>
import { ref, reactive } from 'vue'
import ChildComponentWithSlot from './ChildComponentWithSlot.vue'

const msg = ref('from parent')
</script>

<template>
  <div class="body">
    <ChildComponentWithSlot></ChildComponentWithSlot>

  </div>
</template>