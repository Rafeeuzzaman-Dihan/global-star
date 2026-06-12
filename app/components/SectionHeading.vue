<script setup lang="ts">
defineProps<{
  kicker: string
  heading: string
  subtitle?: string
}>()
</script>

<template>
  <div class="mx-auto max-w-2xl text-center">
    <span class="inline-block rounded-full bg-primary-500/15 px-4 py-1.5 text-xs font-bold uppercase tracking-widest text-primary-400 ring-1 ring-primary-500/30">
      {{ kicker }}
    </span>
    <h2 class="mt-4 text-3xl font-bold tracking-tight text-white sm:text-4xl">{{ heading }}</h2>
    <p v-if="subtitle" class="mt-4 text-base text-ink-muted sm:text-lg">{{ subtitle }}</p>
  </div>
</template>
