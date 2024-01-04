<script setup>
import { ref, onMounted, onBeforeUnmount } from "vue";
import LocalTime from "./LocalTime.vue";
import NewTimeZoneForm from "./NewTimeZoneForm.vue";

const timeZones = ref([]);
let intervalId;

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

onMounted(() => {
  startUpdatingTime();
});

onBeforeUnmount(() => {
  clearInterval(intervalId);
});

function startUpdatingTime() {
  intervalId = setInterval(() => {
    timeZones.value.forEach((timeZone) => {
      const [hours, minutes, seconds] = timeZone.time.split(":").map(Number);
      const newSeconds = (seconds + 1) % 60;
      const newMinutes = minutes + Math.floor((seconds + 1) / 60);
      const newHours = (hours + Math.floor(newMinutes / 60)) % 24;

      timeZone.time = `${String(newHours).padStart(2, "0")}:${String(
        newMinutes
      ).padStart(2, "0")}:${String(newSeconds).padStart(2, "0")}`;
    });
  }, 1000);
}

//Todo:

//Clean up:
// - classnames with BEM
// - complete CSS
</script>

<template>
  <div class="main__watchesRow">
    <div class="card">
      <LocalTime />
      <h3>Your local time</h3>
    </div>
    <div class="card" v-for="timeZone in timeZones" :key="timeZone.id">
      <h2>{{ timeZone.time }}</h2>
      <p>{{ timeZone.location }}</p>
      <button
        class="card__button--delete"
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
