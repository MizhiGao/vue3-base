<script setup>
const props = defineProps({
  msg: String
})
</script>

<template>
    <button class="button">
       {{msg}}
    </button>
</template>