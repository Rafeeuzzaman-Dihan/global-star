<script setup lang="ts">
defineProps<{
  kicker: string
  heading: string
  subtitle?: string
  dark?: boolean
}>()
</script>

<template>
  <div class="mx-auto max-w-2xl text-center">
    <span
      class="inline-block rounded-full px-4 py-1.5 text-xs font-bold uppercase tracking-widest"
      :class="dark
        ? 'bg-primary-500/20 text-primary-300 ring-1 ring-primary-500/30'
        : 'bg-primary-600 text-white shadow-sm shadow-primary-500/30'"
    >
      {{ kicker }}
    </span>
    <h2
      class="mt-5 text-3xl font-extrabold tracking-tight sm:text-4xl"
      :class="dark ? 'text-white' : 'text-slate-900'"
    >{{ heading }}</h2>
    <p v-if="subtitle" class="mt-4 text-base leading-relaxed sm:text-lg" :class="dark ? 'text-slate-400' : 'text-slate-500'">{{ subtitle }}</p>
  </div>
</template>
