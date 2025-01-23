<script setup lang="ts">
import IconStar from "@/assets/icon/IconStar.vue";
defineProps({
  text: {
    type: String,
    required: true,
  },
});
</script>

<template>
  <div class="rating">
    <IconStar />
    <h2>
      {{ text }}
    </h2>
  </div>
</template>

<style lang="scss" scoped>
.rating {
  display: flex;
  align-items: center;

  h2 {
    font-weight: 500;
    font-size: 14px;
    color: darkcyan;
  }
}
</style>
