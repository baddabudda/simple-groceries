<script setup>
import { Icon } from "@iconify/vue";

const emit = defineEmits(["onDeleteAll"]);

function onDeleteAllClicked() {
  emit("onDeleteAll");
}
</script>

<template>
  <div class="toolbar-container">
    <div class="actions-container">
      <div class="test">Simple Groceries</div>
      <button class="button-delete" @click="onDeleteAllClicked">
        <Icon icon="fa6-solid:trash" />
      </button>
    </div>
  </div>
</template>

<style scoped>
.toolbar-container {
  background-color: white;
  height: var(--toolbar-height);
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  border: var(--border-width) solid gray;
}
/* .toolbar-container {
    background-color: white;
    position: fixed;
    height: 3rem;
    top: 0;
    left: 0;
    right: 0;
    border: 1px solid gray;
} */
.actions-container {
  display: grid;
  grid-template-columns: 1fr auto;
}
/* .actions-container {
    display: grid;
    grid-template-columns: 1fr auto;
    padding: 0 1rem;
} */

/* .button-delete {
    aspect-ratio: 1 / 1;
    outline: none;
    cursor: pointer;
    border: none;
} */
</style>
