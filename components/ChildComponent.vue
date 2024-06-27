<script setup>
const props = defineProps({
  msg: String
});

const emit = defineEmits(['updateMessage']);

function updateMessage() {
  emit('updateMessage', 'Hello from Child Component');
}
</script>

<template>
  <div>
    <p>{{ msg }}</p>
    <button class="button" @click="updateMessage">Send Message to Parent</button>
  </div>
</template>