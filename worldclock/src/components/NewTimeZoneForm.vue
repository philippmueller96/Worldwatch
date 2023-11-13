<script setup lang="ts">
import { ref } from "vue";
import { v4 as uuidv4 } from "uuid";

const newLocation = ref("");

const emitAddTimeZone = defineEmits(["addTimeZone"]);

async function addNewTimeZone() {
  const newID = uuidv4();
  try {
    const result = await fetchWorldTime(newLocation.value);
    const newTime = result.hour + ":" + result.minute + ":" + result.second;

    if (newTime) {
      emitAddTimeZone("addTimeZone", newID, newTime, newLocation.value);
      newLocation.value = "";
    }
  } catch (error) {
    console.error("Error fetching world time:", error);
  }
}

async function fetchWorldTime(city) {
  const apiKey = "syrfzxa2LemedbwMWv+o/g==z4C3ZT7OSnh7MgIm";
  const url = `https://api.api-ninjas.com/v1/worldtime?city=${city}`;

  const response = await fetch(url, {
    method: "GET",
    headers: {
      "X-Api-Key": apiKey,
      "Content-Type": "application/json",
    },
  });

  if (!response.ok) {
    throw new Error(`API call failed with status ${response.status}`);
  }

  return await response.json();
}
</script>

<template>
  <div class="newTimeZone">
    <h2>Add New Time Zone</h2>
    <form @submit.prevent="addNewTimeZone">
      <div class="newTimeZone_content">
        <label for="newLocation">Location:</label>
        <input type="text" v-model="newLocation" required />
      </div>
      <button type="submit">Add Time Zone</button>
    </form>
  </div>
</template>
