<script setup lang="ts">
defineProps({
  text: {
    type: String,
    required: true,
  },
});
</script>

<template>
  <h2 class="description">
    {{ text }}
  </h2>
</template>

<style lang="scss" scoped>
.description {
  font-weight: 300;
  font-size: 18px;
  color: black;
  line-height: 30px;
}
</style>
