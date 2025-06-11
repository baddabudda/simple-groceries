<script setup>
import { ref } from "vue";
import { Icon } from "@iconify/vue";

const itemName = ref("");
const itemData = ref("");

const emit = defineEmits(["onSubmit"]);

function onSubmitClicked() {
  let inputSplit = itemName.value.split("\n");

  if (inputSplit[0] !== "") {
    console.log(inputSplit);

    let item = {
      name: inputSplit[0],
      data: inputSplit[1] !== "" ? inputSplit[1] : "",
    };

    emit("onSubmit", item);
    clearInput();
  } else {
    console.log("Trying to submit with empty name");
  }
}

function clearInput() {
  itemName.value = "";
  itemData.value = "";
}
</script>

<template>
  <div class="position-container">
    <div class="add-container">
      <!-- <div class="input-container">
                <input type="text" maxlength="16" class="input name" v-model="itemName" placeholder="Item name...">
                <input type="text" maxlength="16" class="input data" v-model="itemData" placeholder="Item data...">
            </div> -->
      <textarea
        class="input-item"
        v-model="itemName"
        placeholder="Item"
      ></textarea>
      <button class="button-submit" @click="onSubmitClicked">
        <Icon icon="fa6-solid:plus" />
      </button>
    </div>
  </div>
</template>

<style scoped>
.position-container {
  background-color: white;
  height: var(--toolbar-height);
  position: fixed;
  left: 0;
  right: 0;
  bottom: 0;
  border: var(--border-width) solid gray;
  display: flex;
  justify-content: center;
  align-items: center;
}

.add-container {
  max-width: 30rem;
  flex-grow: 1;
  display: flex;
}

.input-item {
  outline: none;
  min-width: 0;
  resize: none;
  flex-grow: 1;
}

</style>
