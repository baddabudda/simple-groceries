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
    <div class="normal-width toolbar-content">
      <div class="toolbar-name">Simple Groceries</div>
      <button class="button" @click="onModeClicked">
        <span style="color: white">{{ props.editModeEnabled ? "EDIT" : "NORMAL"}}</span>
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
  justify-content: center;
}
.toolbar-content {
  display: flex;  
  align-items: baseline;
}
.toolbar-name {
  color: var(--text-primary);
  flex-grow: 1;
}
</style>
