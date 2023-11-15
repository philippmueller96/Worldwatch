<script setup>
import { ref } from "vue";
import Clock from "./Clock.vue";
import NewTimeZoneForm from "./NewTimeZoneForm.vue";
import { v1 as uuidv1 } from "uuid";

const timeZones = ref([
  {
    id: uuidv1(),
    time: "16:16",
    location: "Barcelona",
  },
  {
    id: uuidv1(),
    time: "15:15",
    location: "London",
  },
]);

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

//Search-function when new time gets added
//enter location
//API-Call for current time of location
//check if location exists
//    if not: "location is not available"
//add time and location (new object)
//refresh each time every second

//Clean up:
// - classnames with BEM
// - complete CSS
</script>

<template>
  <div>
    <Clock />
    <button @click="console.log('check')">Add new time</button>
  </div>
  <NewTimeZoneForm @addTimeZone="addNewTime" />
</template>
