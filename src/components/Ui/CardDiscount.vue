<script setup lang="ts">
defineProps({
  text: {
    type: String,
    required: true,
  },
});
</script>

<template>
  <h2 class="discount">Discount {{ text }} %</h2>
</template>

<style lang="scss" scoped>
.discount {
  font-weight: 600;
  font-size: 18px;
  color: darkred;
}

@media (max-width: 767px) {
  .discount {
    font-size: 14px;
  }
}
</style>
