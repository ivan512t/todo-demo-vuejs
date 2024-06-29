<script setup>
import { ref, watchEffect } from "vue";
import Input from "./input.vue";
import Item from "./item.vue";
import { makeStorage } from "./utils.js";

let storage = makeStorage("todos");
let todos = ref(storage.get() ?? []);

watchEffect(() => {
    storage.set(todos.value);
});

function add(newTodo) {
    todos.value.push(newTodo);
}

function remove(id) {
    todos.value = todos.value.filter((todo) => todo.id !== id);
}

function edit(updatedTodo) {
    let index = todos.value.findIndex((todo) => todo.id === updatedTodo.id);
    todos.value[index] = updatedTodo;
}
</script>

<template>
    <div class="pt-16 max-w-sm mx-auto grid gap-6">
        <h1 class="font-bold text-3xl pb-2">Todo Demo Vue.js</h1>
        <Input :add="add" />
        <ul class="grid gap-3">
            <Item v-for="todo in todos" :key="todo.id" :todo="todo" :remove="remove" :edit="edit" />
        </ul>
    </div>
</template>
