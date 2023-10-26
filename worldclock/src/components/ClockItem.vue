<script setup>
export const ClockItemData = {
  name: "ClockItem",
  components: {},
  props: ["clockItem"],
};
</script>

<template>
  <div>
    {{ clockItem.location }}
  </div>
</template>
