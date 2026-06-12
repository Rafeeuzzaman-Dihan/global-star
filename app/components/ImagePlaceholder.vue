<script setup lang="ts">
import { PhotoIcon } from '@heroicons/vue/24/outline'

// Visible placeholder. REPLACE with:
// <img :src="src" :alt="label" class="h-full w-full object-cover rounded-2xl" />
defineProps<{ src: string; label: string }>()
</script>

<template>
  <div
    class="flex h-full w-full flex-col items-center justify-center gap-2.5 rounded-2xl bg-surface-card ring-1 ring-white/10"
    :data-image-src="src"
  >
    <PhotoIcon class="h-10 w-10 text-primary-500/40" />
    <span class="text-xs font-medium text-ink-subtle">{{ label }}</span>
  </div>
</template>
