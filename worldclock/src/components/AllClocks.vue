<script setup>
import Clock from "./Clock.vue";
import ClockItem from "./ClockItem.vue";

export const timeProps = {
  name: "AllClocks",
  components: {
    ClockItem,
  },
  props: ["allTimes"],
};
</script>

<template>
  <div>
    <h2>Your local time</h2>
    <Clock />
    <br />
    <h2>Here we have some clocks</h2>
    <ul>
      <div v-for="time in differentTimes" v-bind:key="time.id">
        <ClockItem v-bind:clockItem="time" />
      </div>
    </ul>
  </div>
</template>
