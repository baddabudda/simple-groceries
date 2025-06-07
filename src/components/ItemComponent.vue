<script setup>
import { ref } from "vue";

const emit = defineEmits(["onItemChecked"]);

const props = defineProps(["item"]);
const checked = ref(props.item.checked);

function onItemChecked() {
  emit("onItemChecked", props.item.id);
  // setTimeout(() => {
  //   emit("onItemChecked", props.item.id);
  // }, 250);
}
</script>

<template>
  <div class="item-container" :class="{ inactive: checked }">
    <div class="item-info">
      <p class="item-name">{{ props.item.item_name }}</p>
      <p class="item-description" v-if="props.item.item_data">
        {{ props.item.item_data }}
      </p>
    </div>
    <input class="checkbox" type="checkbox" :checked="checked" @click="onItemChecked" />
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

.inactive {
  color: gray;
  text-decoration: line-through;
}

.checkbox {
  outline: none;
  width: 20px;
  height: 20px;
}

.checkbox:checked {
  accent-color: green;
}

.item-info {
  flex: 1;
  display: flex;
  flex-direction: column;
  gap: 0.5rem;
}

.item-name {
  color: var(--text-primary);
}

.item-description {
  color: var(--text-secondary);
  font-size: 0.8rem;
}
</style>
