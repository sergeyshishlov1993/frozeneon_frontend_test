<script setup lang="ts">
defineProps({
  text: {
    type: String,
    required: true,
  },
});
</script>

<template>
  <h2 class="brand">
    {{ text }}
  </h2>
</template>

<style lang="scss" scoped>
.brand {
  font-weight: 600;
  font-size: 18px;
  line-height: 1.4;
  color: darkcyan;
}
</style>
