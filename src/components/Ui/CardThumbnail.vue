<script setup lang="ts">
import { ref } from "vue";

const props = defineProps({
  src: {
    type: String,
    required: true,
  },
  alt: {
    type: String,
    default: "Image",
  },
});

const isLoaded = ref<boolean>(false);

function onLoad() {
  isLoaded.value = true;
}
</script>

<template>
  <div class="image-container">
    <img :src="src" :alt="alt" @load="onLoad" class="image" v-show="isLoaded" />

    <div class="skeleton-image" v-show="!isLoaded"></div>
  </div>
</template>

<style lang="scss" scoped>
.image-container {
  width: 100%;
  height: 100%;
  display: flex;
  overflow: hidden;
  position: relative;
  align-items: center;
  justify-content: center;
}

.skeleton-image {
  width: 100%;
  height: 200px;
  filter: blur(0);
  border-radius: 8px;
  background-size: 200% 100%;
  animation: skeleton-loading 1.5s infinite;
  background: linear-gradient(90deg, #fafafa 25%, #f5f5f5 50%, #fafafa 75%);
}

@keyframes skeleton-loading {
  0% {
    background-position: 200% 0;
  }
  100% {
    background-position: -200% 0;
  }
}

.image {
  width: 100%;
  height: 100%;
  object-fit: cover;
  mix-blend-mode: darken;
}
</style>
