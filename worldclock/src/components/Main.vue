<script setup>
import AllClocks from "./AllClocks.vue";

export const differentTimes = [
  {
    id: 1,
    location: "New York, USA",
    time: "check check",
  },
  {
    id: 2,
    location: "Tokyo, Japan",
    time: "check check2",
  },
  {
    id: 3,
    location: "Athens, Greece",
    time: "check check3",
  },
];

</script>

<template>
  <div>
    <AllClocks v-bind="allTimes" />
    <button @click="console.log('check')">Add new time</button>
  </div>
</template>
