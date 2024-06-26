<script>
export default {
  data() {
    return {
      message: 'Hello World!',
      counter: {
        count: 0
      }
    }
  }
}
</script>

<template>
  <body class="body">
    <h1>{{ message }}</h1>
    <p>Count is: {{ counter.count }}</p>
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
.input {
    width: 100px;
}
h1,p {
  padding: 5px;
}
</style>