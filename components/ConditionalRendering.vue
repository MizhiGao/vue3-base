<script setup>
import { ref } from 'vue'

const awesome = ref(true)

function toggle() {
  awesome.value = !awesome.value
}
</script>

<template>
    <body class="body">
        <button @click="toggle" class="button">toggle</button>
        <h1 v-if="awesome">Vue is awesome!</h1>
        <h1 v-else>Oh no 😢</h1>

    </body>
</template>

<style>
.body {
    display: flex;
    flex-direction: column;
    background: rgb(252, 250, 250);
    text-align: center;
    justify-content: center;
    align-items: center;
    height: 150px;
    /* width: 100%; */
}
.button {
  background-color: none;
  border: solid #4CAF50;
  padding: 10px 20px;
  text-align: center;
  text-decoration: none;
  display: inline-block;
  font-size: 16px;
  border-radius: 15px;
}
.button:hover {
  background: #4CAF50;
}
</style>