<script setup>
import { ref } from "vue";
import { makeID } from "./utils.js";

let { add } = defineProps(["add"]);
let text = ref("");

function handleSubmit(event) {
    event.preventDefault();
    let newText = text.value.trim();
    if (!newText) return;
    add({ id: makeID(), text: newText });
    text.value = "";
}
</script>

<template>
    <form @submit="handleSubmit" class="flex gap-2">
        <input
            v-model="text"
            type="text"
            placeholder="Add a new task..."
            class="px-4 py-2 border rounded-md text-sm flex-1"
        />
        <button class="px-4 py-2 bg-[#42b883] text-white rounded-md text-sm font-medium">
            Add
        </button>
    </form>
</template>
