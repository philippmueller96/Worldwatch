<script setup>
import { ref, computed, reactive, onMounted } from "vue";

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
let currentTime = ref(getTime());

const createInterval = () => {
  setInterval(() => {
    currentTime.value = getTime();
  }, 1000);
};
console.log(createInterval());

//To do:
//Need to see time on screen -> check computed on vue-mastery
//refer time to ref to keep it update
//refer it to DOM
</script>

<template>
  <div class="allClocks">
    <h3>{{ currentTime }}</h3>
  </div>
</template>
