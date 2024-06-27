<script setup>
import { ref } from 'vue'

// give each todo a unique id
let id = 0

const newTodo = ref('')
const todos = ref([
  { id: id++, text: 'Learn HTML' },
  { id: id++, text: 'Learn JavaScript' },
])

function addTodo() {
  todos.value.push({ id: id++, text: newTodo.value })
  newTodo.value = ''
}

function removeTodo(todo) {
  todos.value = todos.value.filter((t) => t !== todo)
}
</script>

<template>
    <div class="body">
        <form @submit.prevent="addTodo">
          <input v-model="newTodo">
          <button class="button-remove">Add Todo</button>
        </form>
        <ul>
          <li v-for="todo in todos" :key="todo.id">
            {{ todo.text }}
            <button @click="removeTodo(todo)" class="button-remove">X</button>
          </li>
        </ul>
    </div>
  </template>

<style>
.body{
  display: flex;
    flex-direction: column;
    background: rgb(252, 250, 250);
    text-align: center;
    justify-content: center;
    align-items: center;
    height: 150px;
    /* width: 100%; */
}
.button-remove {
  background-color: none;
  border: 1px solid #4CAF50;
  padding: 0 10px;
  text-align: center;
  text-decoration: none;
  display: inline-block;
  border-radius: 10px;;

}
.button-remove:hover {
  background: #4CAF50;
}
</style>