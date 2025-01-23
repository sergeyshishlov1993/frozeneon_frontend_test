<script setup lang="ts">
defineProps({
  text: {
    type: String,
    required: true,
  },
});
</script>

<template>
  <h2 class="price">$ {{ text }}</h2>
</template>

<style lang="scss" scoped>
.price {
  font-weight: 600;
  font-size: 14px;
  color: darkcyan;
}
</style>
