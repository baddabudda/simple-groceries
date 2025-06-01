<script setup>
import { ref } from 'vue'

const item = ref("")

const emit = defineEmits(["onSubmit"])

function onSubmitClicked() {
    if (item.value !== "") {
        emit("onSubmit", item.value)
        item.value = ""
    }
}
</script>

<template>
    <div class="input-container">
        <input class="input" v-model="item">
        <button class="button submit" @click="onSubmitClicked">Add</button>
    </div>
</template>

<style scoped>
.input-container {
    background-color: gray;
    display: flex;
    flex-direction: row;
    padding: 1rem 0.3rem;
}

.input-container > * {
    font-size: 1.2rem;
}

.input {
    display: block;
    min-width: 0;
    flex: 1;
    padding: 0.1em 0.2em;
    border-radius: 6px 0 0 6px;
    outline: none;
    border-style: solid;
    border-color: gray;
    border-width: 1px 0 1px 1px;
}

.button {
    padding: 0.1em 0.2em;
    flex: 0;
    border-radius: 0 6px 6px 0;
    outline: none;
    border-style: solid;
    border-color: gray;
    border-width: 1px;
    cursor: pointer;
}
</style>