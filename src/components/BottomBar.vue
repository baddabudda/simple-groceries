<script setup>
import { nextTick, ref } from "vue"
import { Icon } from "@iconify/vue"

const extended = ref(false);

const itemName = ref("");
const itemData = ref("");

const dataInput = ref();
const nameInput = ref();

const emit = defineEmits(["onSubmit"]);

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

async function extend() {
  extended.value = true;
  await nextTick();
  if (dataInput.value) {
    dataInput.value.focus();
  }
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
          @keypress.enter.exact="extend"
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
      <button class="form-button extend" @click="extend">
        <Icon icon="fa6-solid:chevron-down" class="icon"/>
      </button>
      <button class="form-button submit" @click="submit">
        <Icon icon="famicons:send" class="icon" />
      </button>
    </div>
  </div>
</template>

<style scoped>
.bottom-bar-container {
  background-color: var(--bg-secondary);
  position: fixed;
  bottom: 0;
  left: 0;
  right: 0;
  display: flex;
  justify-content: center;
  padding: 0.3rem 0;
}
.form-container {
  display: flex;
  flex-grow: 1;
  max-width: var(--max-width-content);
  min-width: 0;
  /* border: 1px solid gray; */
}
.expandable-input {
  display: flex;
  flex-direction: column;
  flex-grow: 1;
  min-width: 0;
}
.form-button {
  background-color: var(--bg-secondary);
  border: none;
  cursor: pointer;
}
.form-button:hover > .icon {
  color: var(--text-primary);
}
.form-input {
  background-color: var(--bg-secondary);
  color: var(--text-primary);
  outline: none;
  border: none;
  padding: 0 0.2rem;
}
</style>
