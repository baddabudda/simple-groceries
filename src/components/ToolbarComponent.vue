<script setup>
import { Icon } from "@iconify/vue";

const emit = defineEmits(["onDeleteAll"]);

function onDeleteAllClicked() {
  emit("onDeleteAll");
}
</script>

<template>
  <div class="toolbar-container">
    <div class="toolbar-name">Simple Groceries</div>
    <div class="actions-container">
      <button class="toolbar-action delete" @click="onDeleteAllClicked">
        <Icon icon="fa6-solid:trash" class="icon" height="1.3rem"/>
      </button>
    </div>
  </div>
</template>

<style scoped>
.toolbar-container {
  background-color: var(--bg-secondary);
  height: var(--top-bar-height);
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  display: flex;
  align-items: center;
  padding: 0 1rem;
}
.toolbar-name {
  color: var(--text-primary);
  flex-grow: 1;
}
.actions-container {
  display: flex;
  align-items: center;
}
.toolbar-action {
  background-color: transparent;
  border: none;
  aspect-ratio: 1 / 1;
  cursor: pointer;
}
.toolbar-action:hover > .icon {
  color: var(--text-primary);
}
</style>
