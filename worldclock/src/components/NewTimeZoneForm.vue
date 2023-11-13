<script setup lang="ts">
import { ref } from "vue";
import { v4 as uuidv4 } from "uuid";

const newTime = ref("");
const newLocation = ref("");

const emitAddTimeZone = defineEmits(["addTimeZone"]);

function addNewTimeZone() {
  const newID = uuidv4();
  if (newTime.value && newLocation.value) {
    emitAddTimeZone("addTimeZone", newID, newTime.value, newLocation.value);
    newTime.value = "";
    newLocation.value = "";
  }
}
</script>

<template>
  <div class="newTimeZone">
    <h2>Add New Time Zone</h2>
    <form @submit.prevent="addNewTimeZone">
      <label for="newTime">Time:</label>
      <input type="text" v-model="newTime" required />

      <label for="newLocation">Location:</label>
      <input type="text" v-model="newLocation" required />

      <button type="submit">Add Time Zone</button>
    </form>
  </div>
</template>
