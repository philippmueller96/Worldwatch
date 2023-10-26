<script setup>
import { ref } from "vue";
import Clock from "./Clock.vue";

let timeZones = ref([
  {
    id: 1,
    time: "16:16",
    location: "Spain",
  },
  {
    id: 2,
    time: "15:15",
    location: "London",
  },
]);

//Todo:
// Button - Add new time
// new component
// opens window and enter Location and time
// add object to other objects
//    --> .push()
// render it

//Button - Delete
// opens window that contains: "Are you sure you want to delete this?"
// remove Object from Array with id
//    --> .pop()
//render it

//Search-function when new time gets added
//enter location
//API-Call for current time of location
//check if location exists
//    if not: "location is not available"
//add time and location (new object)
//refresh each time every second
</script>

<template>
  <div>
    <Clock />
    <div v-for="timeZone in timeZones" :key="timeZone.id">
      <h2>{{ timeZone.time }}</h2>
      <button @click="console.log('delete Time')">Delete</button>
    </div>
    <button @click="console.log('check')">Add new time</button>
  </div>
</template>
