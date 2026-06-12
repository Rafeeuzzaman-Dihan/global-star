<script setup lang="ts">
import type { Component } from 'vue'
import {
  WifiIcon, BuildingOffice2Icon, VideoCameraIcon,
  CodeBracketIcon, WrenchScrewdriverIcon, MegaphoneIcon,
  ArrowRightIcon,
} from '@heroicons/vue/24/outline'
import services from '~/data/services.json'

const icons: Record<string, Component> = {
  WifiIcon, BuildingOffice2Icon, VideoCameraIcon,
  CodeBracketIcon, WrenchScrewdriverIcon, MegaphoneIcon,
}
</script>

<template>
  <section id="services" class="bg-surface py-16 sm:py-20 lg:py-24">
    <div class="mx-auto max-w-7xl px-4 sm:px-6 lg:px-8">
      <SectionHeading :kicker="services.kicker" :heading="services.heading" :subtitle="services.subtitle" />

      <div class="mt-12 grid gap-5 sm:grid-cols-2 lg:grid-cols-3">
        <article
          v-for="service in services.items"
          :key="service.title"
          class="group relative rounded-2xl bg-surface-card p-7 ring-1 ring-white/10 transition-all duration-300 hover:-translate-y-1.5 hover:ring-primary-500/40 hover:shadow-xl hover:shadow-primary-950/60"
        >
          <!-- Top-right corner accent on hover -->
          <div class="absolute right-0 top-0 h-20 w-20 overflow-hidden rounded-2xl opacity-0 transition-opacity group-hover:opacity-100">
            <div class="absolute -right-8 -top-8 h-20 w-20 rounded-full bg-primary-500/15" />
          </div>

          <!-- Icon -->
          <span class="inline-flex h-13 w-13 items-center justify-center rounded-xl bg-primary-500/15 ring-1 ring-primary-500/25 transition-all group-hover:bg-primary-500/25 group-hover:ring-primary-500/50">
            <component :is="icons[service.icon]" class="h-6 w-6 text-primary-400 transition-colors group-hover:text-primary-300" />
          </span>

          <h3 class="mt-5 text-lg font-bold text-white">{{ service.title }}</h3>
          <p class="mt-2 text-sm leading-relaxed text-ink-muted">{{ service.description }}</p>

          <a
            :href="service.link"
            class="mt-5 inline-flex items-center gap-1.5 text-sm font-semibold text-primary-400 transition-all hover:text-primary-300 hover:gap-2.5"
          >
            Read More
            <ArrowRightIcon class="h-4 w-4 transition-transform group-hover:translate-x-1" />
          </a>
        </article>
      </div>
    </div>
  </section>
</template>
