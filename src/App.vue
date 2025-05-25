<script setup>
import { ref } from 'vue';
import ItemComponent from './components/ItemComponent.vue'

// const items = ref([
//   {id: 0, item_name: 'Apple', item_data: '3 medium', bought: false},
//   {id: 1, item_name: 'Banana', item_data: '4', bought: false},
//   {id: 2, item_name: 'Grapes', item_data: '500g', bought: true},
//   {id: 3, item_name: 'Soap', item_data: '1pcs', bought: false},
//   {id: 4, item_name: 'Rope', item_data: '3m', bought: true},
// ])

const items = ref([])

const id_counter = ref(items.value.length)

function addItem() {
  let id = id_counter.value
  items.value.push({id: id, item_name: `Test ${id}`, item_data: 'None', bought: false})
  id_counter.value++
}

function deleteItemById(id) {
  let item_id = items.value.findIndex((item) => item.id == id)
  items.value.splice(item_id, 1)
  console.log(items.value)
}
</script>

<template>
  <button class="add-button" @click="addItem">Add thing</button>
  <div class="container">
    <ItemComponent v-for="item in items" :item :key="item.id" @on-item-checked="deleteItemById"/>
  </div>
</template>

<style scoped>
.add-button {
  width: 100%;
  font-size: 1rem;
  outline: none;
  margin-bottom: 1em;
}

.add-button:hover {
  cursor: pointer;
}

.container {
  display: flex;
  flex-direction: column;
  gap: 0.5em;
}
</style>
