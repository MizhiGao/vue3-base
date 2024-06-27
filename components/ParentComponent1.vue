<script setup>
import { ref } from 'vue';
import ChildComponent from './ChildComponent.vue';

const message = ref('Hello from Parent Component');

function handleUpdateMessage(newMessage) {
  message.value = newMessage;
}
</script>

<template>
  <div class="body">
    <p>{{ message }}</p>
    <ChildComponent :msg="message" @updateMessage="handleUpdateMessage" />
  </div>
</template>