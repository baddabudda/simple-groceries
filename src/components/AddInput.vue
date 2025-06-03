<script setup>
import { ref } from 'vue'

const itemName = ref('')
const itemData = ref('')

const emit = defineEmits(["onSubmit"])

function onSubmitClicked() {
    if (itemName.value !== "") {
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
    <div class="position-container">
        <div class="add-container">
            <div class="input-container">
                <input type="text" maxlength="16" class="input name" v-model="itemName" placeholder="Item name...">
                <input type="text" maxlength="16" class="input data" v-model="itemData" placeholder="Item data...">
            </div>
            <button class="button submit" @click="onSubmitClicked">&plus;</button>
            <button class="button submit" @click="onSubmitClicked">&circlearrowleft;</button>
        </div>
    </div>
</template>

<style scoped>
.position-container {
    background-color: white;
    max-width: 30rem;
    height: 4rem;
    margin: 0 auto;
    position: fixed;
    bottom: 0;
    left: 0;
    right: 0;
}

.add-container {
    height: inherit;
    display: flex;
    flex-direction: row;
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
    outline: none;
    border-width: 0;
    border-style: solid;
    border-color: gray;
}

.name {
    font-size: 1.2rem;
}

.data {
    font-size: 1rem;
}

.button {
    height: 3rem;
    width: 3rem;
    font-size: 1.5rem;
    outline: none;
    border-style: solid;
    border-color: gray;
    border-width: 0;
    cursor: pointer;
    margin: auto 0;
}
</style>