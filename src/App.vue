<script setup>
import { ref } from 'vue';
import ItemComponent from './components/ItemComponent.vue'
import AddItem from './components/AddItem.vue'
import AddInput from './components/AddInput.vue';

const items = ref([])

const id_counter = ref(items.value.length)
const showAddItemDialog = ref(false)

function addItem(item) {
  let id = id_counter.value
  items.value.push({id: id, item_name: item, item_data: "", bought: false})
  id_counter.value++
}

function deleteItemById(id) {
  let item_id = items.value.findIndex((item) => item.id == id)
  items.value.splice(item_id, 1)
  console.log(items.value)
}

function showAddDialog() {
  showAddItemDialog.value = true
}

function handleSubmit(item) {
  showAddItemDialog.value = false
  addItem(item)
}
</script>

<template>
  <div class="main-container">
    <div class="container">
      <ItemComponent v-for="item in items" :item :key="item.id" @on-item-checked="deleteItemById"/>
    </div>
    <AddInput @on-submit="handleSubmit"/>
  </div>
</template>

<style scoped>
.main-container {
  display: flex;
  height: 100vh;
  flex-direction: column;
  overflow: hidden;
}

.add-button:hover {
  cursor: pointer;
}

.container {
  display: flex;
  flex: 1;
  overflow-y: auto;
  flex-direction: column;
  gap: 0.5em;
  padding: 0 0 0.5rem 0;
}
</style>
