<script setup lang="ts">
import type { Component } from 'vue'
import { UsersIcon, BriefcaseIcon, HeartIcon, PhoneIcon } from '@heroicons/vue/24/outline'
import about from '~/data/about.json'

const icons: Record<string, Component> = { UsersIcon, BriefcaseIcon, HeartIcon, PhoneIcon }
</script>

<template>
  <section id="about" class="bg-surface-muted py-16 sm:py-20 lg:py-24">
    <div class="mx-auto max-w-7xl px-4 sm:px-6 lg:px-8">
      <div class="grid items-center gap-14 lg:grid-cols-2">

        <!-- Image placeholder.
             REPLACE ImagePlaceholder with <img src="/images/about/about-team.jpg" ... /> when asset exists. -->
        <div class="order-2 aspect-[4/3] w-full lg:order-1">
          <ImagePlaceholder :src="about.image" :label="about.imageLabel" />
        </div>

        <!-- Copy -->
        <div class="order-1 lg:order-2">
          <span class="inline-block rounded-full bg-primary-500/15 px-4 py-1.5 text-xs font-bold uppercase tracking-widest text-primary-400 ring-1 ring-primary-500/30">
            {{ about.kicker }}
          </span>
          <h2 class="mt-4 text-3xl font-bold tracking-tight text-white sm:text-4xl">{{ about.heading }}</h2>
          <p class="mt-5 text-base leading-relaxed text-ink-muted sm:text-lg">{{ about.text }}</p>

          <!-- Why points -->
          <div class="mt-8 space-y-3">
            <div
              v-for="point in about.whyPoints"
              :key="point.number"
              class="flex gap-5 rounded-2xl bg-surface-card p-5 ring-1 ring-white/10 transition-all hover:ring-primary-500/30 hover:-translate-y-0.5"
            >
              <span class="font-heading text-3xl font-extrabold text-primary-500/30 leading-none">{{ point.number }}</span>
              <div>
                <h3 class="font-semibold text-white">{{ point.title }}</h3>
                <p class="mt-1 text-sm text-ink-muted">{{ point.description }}</p>
              </div>
            </div>
          </div>
        </div>
      </div>

      <!-- Stats -->
      <div class="mt-16 grid grid-cols-2 gap-4 sm:gap-6 lg:grid-cols-4">
        <div
          v-for="stat in about.stats"
          :key="stat.label"
          class="group rounded-2xl bg-surface-card p-6 text-center ring-1 ring-white/10 transition-all hover:-translate-y-1 hover:ring-primary-500/40 hover:shadow-lg hover:shadow-primary-950/50"
        >
          <span class="mx-auto inline-flex h-12 w-12 items-center justify-center rounded-xl bg-primary-500/15 ring-1 ring-primary-500/25">
            <component :is="icons[stat.icon]" class="h-6 w-6 text-primary-400" />
          </span>
          <p class="mt-4 font-heading text-3xl font-extrabold text-white sm:text-4xl">{{ stat.value }}</p>
          <p class="mt-1 text-sm font-medium text-ink-muted">{{ stat.label }}</p>
        </div>
      </div>
    </div>
  </section>
</template>
