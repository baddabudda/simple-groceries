<script setup>
import { ref } from 'vue';

const emit = defineEmits(['onItemChecked'])

const props = defineProps(['item'])
const checked = ref(props.item.bought)

function updateState() {
  props.item.bought = !props.item.bought
  checked.value = props.item.bought
}

function onItemChecked() {
  updateState()
  // console.log(props.item.id)
  setTimeout(() => { emit('onItemChecked', props.item.id) }, 250)
}
</script>

<template>
    <div class="item-container" :class="{inactive: checked}">
      <div class="item-info">
        <p class="item-name">{{ props.item.item_name }}</p>
        <p class="item-description" v-if="props.item.item_data !== ''">{{ props.item.item_data }}</p>
      </div>
      <input class="checkbox" type="checkbox" @click="onItemChecked">
    </div>
</template>

<style scoped>
.item-container {
  display: flex;
  flex-direction: row;
  align-items: center;
  border-color: grey;
  border-style: solid;
  border-width: 1px;
  border-radius: 6px;
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

.item-description {
  font-size: 0.8rem;
}
</style>
