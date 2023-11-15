<script setup>
import { ref } from "vue";
import Clock from "./Clock.vue";
import NewTimeZoneForm from "./NewTimeZoneForm.vue";
import { v1 as uuidv1 } from "uuid";

const timeZones = ref([]);

function addNewTime(newID, newTime, newLocation) {
  timeZones.value.push({
    id: newID,
    time: newTime,
    location: newLocation,
  });
  console.log(timeZones.value);
}

function deleteClock(id) {
  const index = timeZones.value.findIndex((timeZone) => timeZone.id === id);

  if (index !== -1) {
    timeZones.value.splice(index, 1);
  }
}

//Todo:
// Button - Add new time
// opens window and enter Location and time

//refresh each time every second

//Clean up:
// - classnames with BEM
// - complete CSS
</script>

<template>
  <div class="clockRow">
    <div class="card">
      <Clock />
      <h3>Your local time</h3>
    </div>
    <div class="card" v-for="timeZone in timeZones" :key="timeZone.id">
      <h2>{{ timeZone.time }}</h2>
      <p>{{ timeZone.location }}</p>
      <button
        class="deleteBtn"
        @click="
          console.log('delete Time clicked');
          deleteClock(timeZone.id);
        "
      >
        Delete
      </button>
    </div>
  </div>
  <NewTimeZoneForm @addTimeZone="addNewTime" />
</template>
