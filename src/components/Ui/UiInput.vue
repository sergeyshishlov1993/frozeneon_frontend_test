<script setup lang="ts">
const props = defineProps<{
  type?: string;
  placeholder?: string;
  value?: string;
}>();
</script>

<template>
  <input
    :type="props.type"
    :placeholder="props.placeholder"
    :value="props.value"
  />
</template>

<style lang="scss" scoped>
input {
  width: 100%;
  padding: 20px;
  height: 50px;
  background: rgba(255, 255, 255, 0.3);
  border-radius: 16px;
  box-shadow: 0 4px 30px rgba(0, 0, 0, 0.1);
  backdrop-filter: blur(5.6px);
  border: 1px solid rgba(255, 255, 255, 0.28);
  box-sizing: border-box;
}
</style>
