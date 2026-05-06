<script setup lang="ts">
defineProps<{
  src: string
  alt: string
  width?: string
}>()
</script>

<template>
  <img
    :src="src"
    :alt="alt"
    :style="{ width: width || '100%' }"
    class="mx-auto"
  >
</template>
