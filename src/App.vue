<script setup>
import { ref, onMounted } from "vue";
import ItemComponent from "./components/ItemComponent.vue";
import ToolbarComponent from "./components/ToolbarComponent.vue";
import BottomBar from "./components/BottomBar.vue";

const items = ref([]);
const currentId = ref(-1);

const itemsKey = "items";
const idKey = "last_id";

onMounted(() => {
  if (localStorage.getItem(itemsKey)) {
    items.value = JSON.parse(localStorage.getItem(itemsKey));
    currentId.value = JSON.parse(localStorage.getItem(idKey));
  }
});

function addItem(item) {
  currentId.value++;
  items.value.push({
    id: currentId.value,
    item_name: item.name,
    item_data: item.data,
    checked: false,
  });
  saveItem();
}

function deleteItemById(id) {
  let item_id = items.value.findIndex((item) => item.id == id)
  items.value.splice(item_id, 1);
  saveItem();
  console.log(items.value);
}

function handleSubmit(item) {
  addItem(item);
}

function saveItem() {
  const parsed = JSON.stringify(items.value);
  localStorage.setItem(itemsKey, parsed);
  localStorage.setItem(idKey, currentId.value);
}

function deleteAll() {
  console.log("Cleaning...");
  localStorage.clear();
  resetValues();
}

function resetValues() {
  currentId.value = -1;
  items.value = [];
}

function handleCheck(id) {
  let item_id = items.value.findIndex((item) => item.id === id)
  items.value[item_id].checked = !items.value[item_id].checked
  saveItem()
}
</script>

<template>
  <ToolbarComponent @on-delete-all="deleteAll" />
  <div class="main-container">
    <div class="container">
      <ItemComponent
        v-for="item in items"
        :item
        :key="item.id + item.checked"
        @on-item-checked="handleCheck"
      />
    </div>
  </div>
  <BottomBar @on-submit="handleSubmit" />
</template>

<style scoped>
.main-container {
  min-height: 100vh;
  min-height: 100dvh;
  max-width: var(--max-width-content);
  padding-bottom: calc(var(--bottom-bar-height) + 0.5rem);
  padding-left: 0.5rem;
  padding-right: 0.5rem;
  padding-top: calc(var(--top-bar-height) + 0.5rem);
  margin: auto;
}

.container {
  display: flex;
  flex-direction: column;
  gap: 0.5em;
}
</style>
