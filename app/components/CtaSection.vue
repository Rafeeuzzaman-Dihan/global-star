<script setup lang="ts">
import { ArrowRightIcon, SparklesIcon } from '@heroicons/vue/24/outline'
import site from '~/data/site.json'

const { cta } = site
</script>

<template>
  <section class="relative overflow-hidden py-20 sm:py-24">
    <!-- Gradient background -->
    <div class="absolute inset-0 bg-gradient-to-br from-primary-700 via-primary-600 to-secondary-700" />
    <!-- Dot grid overlay -->
    <div class="hero-grid-bg absolute inset-0 opacity-30" />
    <!-- Glow orbs -->
    <div class="pointer-events-none absolute -top-20 -left-20 h-72 w-72 rounded-full bg-primary-400/20 blur-3xl" />
    <div class="pointer-events-none absolute -bottom-20 -right-20 h-72 w-72 rounded-full bg-secondary-500/20 blur-3xl" />

    <div class="relative mx-auto max-w-7xl px-4 sm:px-6 lg:px-8">
      <div class="flex flex-col items-center gap-8 text-center lg:flex-row lg:justify-between lg:text-left">
        <div>
          <span class="inline-flex items-center gap-2 rounded-full bg-white/15 px-4 py-1.5 text-xs font-bold uppercase tracking-widest text-white/90 ring-1 ring-white/25">
            <SparklesIcon class="h-3.5 w-3.5" />
            Get Started Today
          </span>
          <h2 class="mt-4 text-3xl font-bold tracking-tight text-white sm:text-4xl">{{ cta.title }}</h2>
          <p class="mt-3 max-w-xl text-base text-white/70 sm:text-lg">{{ cta.subtitle }}</p>
        </div>
        <a
          :href="cta.button.href"
          class="inline-flex shrink-0 items-center gap-2.5 rounded-2xl bg-white px-8 py-4 text-sm font-bold text-primary-700 shadow-2xl transition-all hover:bg-primary-50 hover:scale-105 hover:shadow-white/20"
        >
          {{ cta.button.label }}
          <ArrowRightIcon class="h-4 w-4" />
        </a>
      </div>
    </div>
  </section>
</template>
