<script setup>
import { Icon } from "@iconify/vue";

const emit = defineEmits(["onDeleteAll", "onChangeMode"]);
const props = defineProps(["editModeEnabled"]);

function onModeClicked() {
  emit("onChangeMode");
}
</script>

<template>
  <div class="toolbar-container">
    <div class="normal-width">
      <div class="toolbar-name">Simple Groceries</div>
      <div class="actions-container">
        <button class="toolbar-action" @click="onModeClicked">
          <span style="color: white">Edit mode: </span>
          <span style="color: white">{{ props.editModeEnabled ? "On" : "Off"}}</span>
        </button>
      </div>
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
  justify-content: center;
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
  cursor: pointer;
}
.toolbar-action:hover > .icon {
  color: var(--text-primary);
}
</style>
