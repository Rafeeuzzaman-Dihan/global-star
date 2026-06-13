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

      <div class="mt-12 grid gap-6 sm:grid-cols-2 lg:grid-cols-3">
        <article
          v-for="service in services.items"
          :key="service.title"
          class="group relative flex flex-col overflow-hidden rounded-2xl bg-white p-7 shadow-sm ring-1 ring-slate-200/80 transition-all duration-300 hover:-translate-y-1 hover:shadow-lg hover:ring-primary-200"
        >
          <!-- Top accent bar that appears on hover -->
          <div class="absolute inset-x-0 top-0 h-0.5 bg-gradient-to-r from-primary-500 to-primary-400 opacity-0 transition-opacity duration-300 group-hover:opacity-100" />

          <!-- Icon -->
          <span class="inline-flex h-13 w-13 items-center justify-center rounded-xl bg-primary-100 ring-1 ring-primary-200 transition-all group-hover:bg-primary-600 group-hover:ring-primary-600 group-hover:shadow-md group-hover:shadow-primary-200">
            <component :is="icons[service.icon]" class="h-6 w-6 text-primary-700 transition-colors group-hover:text-white" />
          </span>

          <h3 class="mt-5 text-lg font-bold text-slate-900">{{ service.title }}</h3>
          <p class="mt-2 flex-1 text-sm leading-relaxed text-slate-500">{{ service.description }}</p>

          <a
            :href="service.link"
            class="mt-6 inline-flex items-center gap-1.5 text-sm font-semibold text-primary-600 transition-all hover:gap-3 hover:text-primary-700"
          >
            Read More
            <ArrowRightIcon class="h-4 w-4" />
          </a>
        </article>
      </div>
    </div>
  </section>
</template>
