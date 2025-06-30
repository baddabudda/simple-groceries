<script setup>
import { ref, onMounted } from "vue";
import ItemComponent from "./components/ItemComponent.vue";
import ToolbarComponent from "./components/ToolbarComponent.vue";
import BottomBar from "./components/BottomBar.vue";

const items = ref([]);
const currentId = ref(-1);
const editModeEnabled = ref(false);

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

function handleDeleteById(id) {
  let item_id = items.value.findIndex((item) => item.id === id)
  console.log(item_id)
  items.value.splice(item_id, 1)
  saveItem()
}

function changeMode() {
  editModeEnabled.value = !editModeEnabled.value;
}
</script>

<template>
  <ToolbarComponent :editModeEnabled @on-delete-all="deleteAll" @on-change-mode="changeMode"/>
  <div class="main-container">
    <!-- <button v-if="editModeEnabled" class="delete-button" @click="deleteAll">Delete all</button> -->
    <div class="normal-width container-list">
      <ItemComponent
        v-for="item in items"
        :item
        :editModeEnabled
        :key="item.id + item.checked"
        @on-item-checked="handleCheck"
        @on-item-delete-pressed="handleDeleteById"
      />
    </div>
  </div>
  <BottomBar :editModeEnabled @on-submit="handleSubmit" @on-delete-all="deleteAll"/>
</template>

<style scoped>
.main-container {
  min-height: 100vh;
  min-height: 100dvh;
  max-width: var(--max-width-content);
  padding-bottom: calc(var(--max-bottom-bar-height) + 0.5rem);
  padding-top: calc(var(--top-bar-height) + 0.5rem);
  margin: auto;
}

.container-list {
  display: flex;
  flex-direction: column;
  gap: 0.5em;
}

.delete-button {
  width: 100%;
  background-color: transparent;
  color: white;
  border: 1px solid gray;
  border-radius: 2px;
  margin-bottom: 0.5rem;
  cursor: pointer;
}
</style>
