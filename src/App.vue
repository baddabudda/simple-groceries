<script setup>
import { ref, onMounted } from 'vue';
import ItemComponent from './components/ItemComponent.vue'
import AddInput from './components/AddInput.vue';

const items = ref([])
const currentId = ref(-1)

const itemsKey = "items"
const idKey = "last_id"

onMounted(() => {
  if (localStorage.getItem(itemsKey)) {
    items.value = JSON.parse(localStorage.getItem(itemsKey))
    currentId.value = JSON.parse(localStorage.getItem(idKey))
  }
})

function addItem(item) {
  currentId.value++
  items.value.push({id: currentId.value, item_name: item.name, item_data: item.data,bought: false})
  saveItem()
}

function deleteItemById(id) {
  let item_id = items.value.findIndex((item) => item.id == id)
  items.value.splice(item_id, 1)
  saveItem()
  console.log(items.value)
}

function handleSubmit(item) {
  addItem(item)
}

function saveItem() {
  const parsed = JSON.stringify(items.value)
  localStorage.setItem(itemsKey, parsed)
  localStorage.setItem(idKey, currentId.value)
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
  height: 100vh;
  height: 100dvh;
  max-width: 30rem;
  margin: auto;
}

.add-button:hover {
  cursor: pointer;
}

.container {
  display: flex;
  flex: 1;
  flex-direction: column;
  gap: 0.5em;
  padding: 0.5rem 0 4.5rem 0;
}
</style>
