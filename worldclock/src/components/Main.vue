<script setup>
import Clock from "./Clock.vue";
</script>

<template>
  <div>
    <Clock />
    <button @click="console.log('check')">Add new time</button>
  </div>
</template>
