<script setup>
import { nextTick, ref } from "vue";

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
  <div class="form-container">
    <div class="expandable-input">
      <input
        @keypress.ctrl.enter.exact="submit"
        @keypress.enter.exact="extend"
        v-model="itemName"
        ref="nameInput"
        type="text"
      />
      <!-- <input class="data-input" @keypress.enter="submit" v-show="extended" ref="dataInput" v-model="itemData" type="text"><br v-show="extended"> -->
      <input
        class="data-input"
        @keypress.enter="submit"
        v-show="extended"
        ref="dataInput"
        v-model="itemData"
        type="text"
      />
    </div>
    <button @click="extend">Extend</button><br />
    <button class="submit-button" @click="submit">Submit</button>
  </div>
</template>

<style scoped>
.form-container {
  display: flex;
}
.expandable-input {
  display: flex;
  flex-direction: column;
}
</style>
