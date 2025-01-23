<script setup lang="ts">
defineProps({
  text: {
    type: String,
    required: true,
  },
});
</script>

<template>
  <div class="category-wrapper">
    <h2 class="category">
      {{ text }}
    </h2>
  </div>
</template>

<style lang="scss" scoped>
.category-wrapper {
  padding: 6px 8px;
  background: black;
  border-radius: 20px;
}
.category {
  font-weight: 500;
  font-size: 12px;
  color: greenyellow;
}
</style>
