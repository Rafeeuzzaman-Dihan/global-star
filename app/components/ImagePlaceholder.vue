<script setup lang="ts">
import { PhotoIcon } from '@heroicons/vue/24/outline'

// Visible placeholder. REPLACE with:
// <img :src="src" :alt="label" class="h-full w-full object-cover rounded-xl" />
defineProps<{ src: string; label: string }>()
</script>

<template>
  <div
    class="flex h-full w-full flex-col items-center justify-center gap-2.5 rounded-xl bg-gradient-to-br from-slate-100 to-blue-50"
    :data-image-src="src"
  >
    <div class="flex h-12 w-12 items-center justify-center rounded-full bg-white shadow-sm">
      <PhotoIcon class="h-6 w-6 text-primary-400" />
    </div>
    <span class="text-xs font-medium text-slate-400">{{ label }}</span>
  </div>
</template>
