<script setup>
import { ref } from 'vue'

const itemName = ref('')
const itemData = ref('')

const emit = defineEmits(["onSubmit"])

function onSubmitClicked() {
    if (itemName !== "") {
        let item = {
            name: itemName.value,
            data: itemData.value
        }

        emit("onSubmit", item)
        clearInput()
    }
}

function clearInput() {
    itemName.value = ''
    itemData.value = ''
}
</script>

<template>
    <div class="add-container">
        <div class="input-container">
            <input type="text" maxlength="16" class="input name" v-model="itemName" placeholder="Item name...">
            <input type="text" maxlength="16" class="input data" v-model="itemData" placeholder="Item data...">
        </div>
        <button class="button submit" @click="onSubmitClicked">Add</button>
    </div>
</template>

<style scoped>
.add-container {
    background-color: white;
    display: flex;
    flex-direction: row;
    padding: 0.1rem 0.2rem;
}

.input-container {
    width: 0;
    flex: 1;
    display: flex;
    flex-direction: column;
}

.input {
    display: block;
    min-width: 0;
    flex: 1;
    padding: 0.1em 0.2em;
    outline: none;
    border-width: 0;
    border-style: solid;
    border-color: gray;
}

.name {
    border-width: 1px 0 0 1px;
    border-radius: 6px 0 0 0;
    font-size: 1.2rem;
}

.data {
    border-width: 0 0 1px 1px;
    border-radius: 0 0 0 6px;
    font-size: 1rem;
}

.button {
    padding: 0.1em 0.2em;
    flex: 0 10%;
    border-radius: 0 6px 6px 0;
    outline: none;
    border-style: solid;
    border-color: gray;
    border-width: 1px;
    cursor: pointer;
}
</style>