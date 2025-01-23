<script setup lang="ts">
defineProps({
  text: {
    type: String,
    required: true,
  },
});
</script>

<template>
  <h2 class="title">
    {{ text }}
  </h2>
</template>

<style lang="scss" scoped>
.title {
  font-weight: 500;
  font-size: 22px;
  color: black;
}
</style>
