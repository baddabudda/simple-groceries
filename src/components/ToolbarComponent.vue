<script setup>
const emit = defineEmits(["onDeleteAll"])

function onDeleteAllClicked() {
    emit("onDeleteAll")
}
</script>

<template>
    <div class="toolbar-container">
        <div class="actions-container">
            <button class="button delete" @click="onDeleteAllClicked">&times;</button>
        </div>
    </div>
</template>

<style scoped>
.toolbar-container {
    background-color: aqua;
    position: fixed;
    left: 0;
    right: 0;
    height: 3rem;
    width: 30rem;
    margin: 0 auto;
}

.actions-container {
    display: flex;
    justify-content: center;
}

.button {
    font-size: 1.5rem;
    height: 3rem;
    width: 3rem;
    outline: none;
    cursor: pointer;
    border-style: solid;
    border-width: 0;
    border-radius: 0;
}
</style>