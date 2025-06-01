<script setup>
import { ref } from 'vue'

const emit = defineEmits(["onSubmit"])

const itemName = ref("")
const itemInfo = ref("")

function onSubmitClicked() {
    let item = {
        name: itemName.value,
        info: itemInfo.value
    }
    emit("onSubmit", item)
}
</script>

<template>
    <div class="dialog-container">
        <div class="form">
            <p>Add new item!</p>
            <input class="form-input" type="text" placeholder="Item name" v-model="itemName">
            <input class="form-input" type="text" placeholder="Amount (e.g. 10pcs or 100g)" v-model="itemInfo">
            <div class="button-panel">
                <button class="form-button" @click="onSubmitClicked">Add</button>
                <button class="form-button" @click="onSubmitClicked">Cancel</button>
            </div>
        </div>
    </div>
</template>

<style scoped>
.form {
    background-color: aqua;
    display: flex;
    flex-direction: column;
    gap: 0.5em;
    padding: 0.5em 1em;
    border-radius: 4px;
    border-width: 1px;
    border-style: solid;
    border-color: gray;
}

.form-input {
    outline: none;
    font-size: 1rem;
    padding: 0 0.2rem;
}

.button-panel {
    display: flex;
    gap: 0.5em;
    justify-content: center;
}

.form-button {
    font-size: 0.8rem;
}
</style>