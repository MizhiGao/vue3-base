<script>
export default {
  data() {
    return {
      count: 0
    }
  },
  methods: {
    increment() {
      this.count++
    }
  }
}
</script>

<template>
  <button class="button"
    @click="increment">count is: {{ count }}</button>
</template>

<style>
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