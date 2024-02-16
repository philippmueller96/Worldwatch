<script setup>
import { ref } from "vue";

const getTime = () => {
  let today = new Date();
  let hours = today.getHours();
  let minutes = today.getMinutes();
  let seconds = today.getSeconds();
  return (
    hours +
    ":" +
    (minutes < 10 ? "0" : "") +
    minutes +
    ":" +
    (seconds < 10 ? "0" : "") +
    seconds
  );
};

console.log(getTime());
let localTime = ref(getTime());

const createInterval = () => {
  setInterval(() => {
    localTime.value = getTime();
  }, 1000);
};
console.log(createInterval());
</script>

<template>
  <div>
    <h3>{{ localTime }}</h3>
  </div>
</template>
