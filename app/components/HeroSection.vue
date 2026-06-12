<script setup lang="ts">
import type { Component } from 'vue'
import { ShieldCheckIcon, ClockIcon, BoltIcon } from '@heroicons/vue/24/outline'
import { ChevronRightIcon } from '@heroicons/vue/20/solid'
import site from '~/data/site.json'

const { hero } = site
const icons: Record<string, Component> = { ShieldCheckIcon, ClockIcon, BoltIcon }
</script>

<template>
  <section id="home" class="relative min-h-screen overflow-hidden bg-surface">
    <!-- Dot-grid background -->
    <div class="hero-grid-bg absolute inset-0 opacity-70" />
    <!-- Radial top glow -->
    <div class="hero-radial-glow pointer-events-none absolute inset-0" />
    <!-- Bottom fade into next section -->
    <div class="pointer-events-none absolute inset-x-0 bottom-0 h-40 bg-gradient-to-t from-surface to-transparent" />

    <div class="relative mx-auto flex min-h-screen max-w-7xl items-center px-4 pt-16 pb-10 sm:px-6 lg:px-8">
      <div class="grid w-full items-center gap-14 lg:grid-cols-2">

        <!-- ── Left: copy ─────────────────────────────────────── -->
        <div class="text-center lg:text-left">
          <!-- Badge -->
          <span class="inline-flex items-center gap-2 rounded-full bg-primary-500/10 px-4 py-2 text-xs font-bold uppercase tracking-widest text-primary-400 ring-1 ring-primary-500/30">
            <BoltIcon class="h-3.5 w-3.5" />
            {{ hero.badge }}
          </span>

          <!-- Heading with gradient text -->
          <h1 class="mt-6 bg-gradient-to-br from-white via-primary-200 to-primary-400 bg-clip-text text-4xl font-extrabold leading-[1.1] tracking-tight text-transparent sm:text-5xl lg:text-[3.6rem]">
            {{ hero.headline }}
          </h1>

          <p class="mx-auto mt-6 max-w-xl text-base leading-relaxed text-ink-muted sm:text-lg lg:mx-0">
            {{ hero.subtext }}
          </p>

          <!-- CTAs -->
          <div class="mt-8 flex flex-col items-center gap-4 sm:flex-row sm:justify-center lg:justify-start">
            <a
              :href="hero.primaryCta.href"
              class="btn-glow inline-flex w-full items-center justify-center gap-2 rounded-xl bg-primary-600 px-7 py-3.5 text-sm font-semibold text-white transition-all hover:bg-primary-500 sm:w-auto"
            >
              {{ hero.primaryCta.label }}
              <ChevronRightIcon class="h-4 w-4" />
            </a>
            <a
              :href="hero.secondaryCta.href"
              class="inline-flex w-full items-center justify-center rounded-xl px-7 py-3.5 text-sm font-semibold text-ink transition-all ring-1 ring-white/20 hover:bg-white/8 hover:text-white sm:w-auto"
            >
              {{ hero.secondaryCta.label }}
            </a>
          </div>

          <!-- Trust strip -->
          <ul class="mt-10 flex flex-wrap items-center justify-center gap-x-8 gap-y-3 lg:justify-start">
            <li
              v-for="item in hero.trustStrip"
              :key="item.label"
              class="flex items-center gap-2 text-sm font-medium text-ink-muted"
            >
              <component :is="icons[item.icon]" class="h-4.5 w-4.5 text-primary-400" />
              {{ item.label }}
            </li>
          </ul>
        </div>

        <!-- ── Right: image placeholder ──────────────────────── -->
        <!-- REPLACE ImagePlaceholder with <img src="/images/hero/hero-main.jpg" ... /> when asset exists. -->
        <div class="relative mx-auto w-full max-w-lg lg:max-w-none">
          <!-- Glow ring behind the image -->
          <div class="absolute -inset-4 rounded-3xl bg-primary-600/20 blur-2xl" />
          <div class="relative aspect-[4/3] overflow-hidden rounded-2xl ring-1 ring-primary-500/30">
            <ImagePlaceholder :src="hero.image" :label="hero.imageLabel" />
          </div>
          <!-- Floating stat chip — top-right -->
          <div class="absolute -top-4 -right-4 hidden rounded-2xl bg-surface-elevated px-4 py-3 text-center ring-1 ring-white/10 shadow-xl lg:block">
            <p class="font-heading text-2xl font-extrabold text-white">5K+</p>
            <p class="text-xs text-ink-muted">Subscribers</p>
          </div>
          <!-- Floating stat chip — bottom-left -->
          <div class="absolute -bottom-4 -left-4 hidden rounded-2xl bg-surface-elevated px-4 py-3 text-center ring-1 ring-white/10 shadow-xl lg:block">
            <p class="font-heading text-2xl font-extrabold text-primary-400">99.9%</p>
            <p class="text-xs text-ink-muted">Uptime SLA</p>
          </div>
        </div>

      </div>
    </div>
  </section>
</template>
