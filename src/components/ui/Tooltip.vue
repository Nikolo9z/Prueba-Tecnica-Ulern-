<script setup lang="ts">
import { ref } from 'vue'

defineProps<{ text: string }>()

const isVisible = ref(false)
</script>

<template>
  <div
    class="relative inline-block cursor-pointer"
    @mouseenter="isVisible = true"
    @mouseleave="isVisible = false"
  >
    <slot></slot>
    <div
      v-if="isVisible"
      class="absolute bottom-full left-1/2 transform -translate-x-1/2 mb-2 px-3 py-2 text-sm font-medium bg-gray-900 rounded-lg shadow-lg transition-opacity duration-300 z-50"
    >
      {{ text }}
    </div>
  </div>
</template>
