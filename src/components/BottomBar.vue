<script setup>
import { nextTick, ref } from "vue"
import { Icon } from "@iconify/vue"

const extended = ref(false);

const itemName = ref("");
const itemData = ref("");

const dataInput = ref();
const nameInput = ref();

const expandIcon = ref();

const emit = defineEmits(["onSubmit"]);

const icons = {
  expand: "fa6-solid:chevron-up",
  collapse: "fa6-solid:chevron-up" 
}

function submit() {
  if (nameInput.value) {
    nameInput.value.focus();
  }
  if (itemName.value) {
    let item = {
      name: itemName.value,
      data: itemData.value,
    };
    clearInput();
    emit("onSubmit", item);
  } else {
    console.log("Trying to submit with empty name");
  }
}

async function handleExpand() {
  if (extended.value === false) {
    console.log('expand')
    extended.value = true
    await nextTick()
    focusOnDataInput()
  } else {
    extended.value = false
    await nextTick()
    focusOnNameInput()
  }
}

function focusOnDataInput() {
  if (dataInput.value) {
    dataInput.value.focus()
  }
}

function focusOnNameInput() {
  nameInput.value.focus()
} 

function clearInput() {
  itemName.value = "";
  itemData.value = "";
  extended.value = false;
}
</script>

<template>
  <div class="bottom-bar-container">
    <!-- <InfoInput/> -->
    <div class="form-container">
      <div class="expandable-input">
        <input
          class="form-input name"
          @keypress.ctrl.enter.exact="submit"
          @keypress.enter.exact="handleExpand"
          v-model="itemName"
          ref="nameInput"
          type="text"
          placeholder="item"
        />
        <!-- <input class="data-input" @keypress.enter="submit" v-show="extended" ref="dataInput" v-model="itemData" type="text"><br v-show="extended"> -->
        <input
          class="form-input data"
          @keypress.enter="submit"
          v-show="extended"
          ref="dataInput"
          v-model="itemData"
          type="text"
          placeholder="info"
        />
      </div>
      <div class="button-group">
        <button class="form-button extend" @click="handleExpand">
          <Icon v-if="!extended" icon="fa6-solid:chevron-down" class="icon" height="1.3rem"/>
          <Icon v-if="extended" icon="fa6-solid:chevron-up" class="icon" height="1.3rem"/>
        </button>
        <button class="form-button submit" @click="submit">
          <Icon icon="famicons:send" class="icon" height="1.3rem"/>
        </button>
      </div>
    </div>
  </div>
</template>

<style scoped>
.bottom-bar-container {
  background-color: var(--bg-secondary);
  max-height: var(--bottom-bar-height);
  position: fixed;
  bottom: 0;
  left: 0;
  right: 0;
  display: flex;
  justify-content: center;
  align-items: center;
  padding: 0.5rem 0.5rem;
}
.form-container {
  display: flex;
  flex-grow: 1;
  max-width: var(--max-width-content);
  min-width: 0;
}
.expandable-input {
  display: flex;
  flex-direction: column;
  flex-grow: 1;
  min-width: 0;
  justify-content: center;
  gap: 0.5rem;
}
.form-input {
  background-color: var(--bg-secondary);
  color: var(--text-primary);
  outline: none;
  border: none;
  padding: 0 0.2rem;
}
.button-group {
  display: flex;
  gap: 1rem;
  align-items: center;
}
.form-button {
  background-color: var(--bg-secondary);
  height: 2rem;
  aspect-ratio: 1 / 1;
  border: none;
  cursor: pointer;
}
.form-button:hover > .icon {
  color: var(--text-primary);
}
</style>
