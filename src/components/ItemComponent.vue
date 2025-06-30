<script setup>
import { Icon } from "@iconify/vue";
import { ref } from "vue";

const emit = defineEmits(["onItemChecked", "onItemDeletePressed"]);

const props = defineProps(["item"]);
const checked = ref(props.item.checked);

function onItemChecked() {
  emit("onItemChecked", props.item.id);
  // setTimeout(() => {
  //   emit("onItemChecked", props.item.id);
  // }, 250);
}

function onItemDeletePressed() {
  emit("onItemDeletePressed", props.item.id);
}
</script>

<template>
  <div class="item-container">
    <div class="item-info" >
      <p class="item-name" :class="{ inactive: checked }">{{ props.item.item_name }}</p>
      <p class="item-description" v-if="props.item.item_data" :class="{ inactive: checked}">
        {{ props.item.item_data }}
      </p>
    </div>
    <div class="actionbar-end">
      <input class="checkbox" type="checkbox" :checked="checked" @click="onItemChecked" />
      <button class="icon-button" @click="onItemDeletePressed">
        <Icon icon="fa-solid:times" class="icon" />
      </button>
    </div>
  </div>
</template>

<style scoped>
.item-container {
  background-color: var(--bg-primary);
  display: flex;
  flex-direction: row;
  align-items: center;
  border: 1px solid var(--border);
  border-radius: 0.5em;
  padding: 0.5em 1em;
}

.actionbar-end {
  display: flex;
  gap: 0.8em;
  align-items: center;
}

.checkbox {
  outline: none;
  width: 20px;
  aspect-ratio: 1 / 1;
}

.checkbox:checked {
  accent-color: green;
}

.action-delete {
  text-align: center;
  background-color: transparent;
  width: 20px;
  aspect-ratio: 1 / 1;
  border: none;
  border-radius: 2px;
  padding: 0;
  display: flex;
  align-items: center;
  justify-content: center;
}

.item-info {
  flex: 1;
  display: flex;
  flex-direction: column;
  gap: 0.5rem;
  overflow: hidden;
}

.item-name {
  color: var(--text-primary);
}

.item-description {
  color: var(--text-secondary);
  font-size: 0.8rem;
}

.inactive {
  color: var(--inactive);
  text-decoration: line-through;
}
</style>
