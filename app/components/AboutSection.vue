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

        <!-- Image -->
        <div class="order-2 aspect-[4/3] w-full overflow-hidden rounded-2xl shadow-xl lg:order-1">
          <img src="/about.jpg" :alt="about.imageLabel" class="h-full w-full object-cover" />
        </div>

        <!-- Copy -->
        <div class="order-1 lg:order-2">
          <span class="inline-block rounded-full bg-primary-600 px-4 py-1.5 text-xs font-bold uppercase tracking-widest text-white shadow-sm shadow-primary-500/30">
            {{ about.kicker }}
          </span>
          <h2 class="mt-5 text-3xl font-extrabold tracking-tight text-slate-900 sm:text-4xl">{{ about.heading }}</h2>
          <p class="mt-4 text-base leading-relaxed text-slate-500 sm:text-lg">{{ about.text }}</p>

          <!-- Why points -->
          <div class="mt-8 space-y-3">
            <div
              v-for="point in about.whyPoints"
              :key="point.number"
              class="flex gap-5 rounded-xl border border-slate-200 bg-white p-5 shadow-sm transition-all hover:-translate-y-0.5 hover:border-primary-200 hover:shadow-md"
            >
              <span class="shrink-0 font-heading text-3xl font-extrabold leading-none text-primary-200">{{ point.number }}</span>
              <div>
                <h3 class="font-semibold text-slate-900">{{ point.title }}</h3>
                <p class="mt-1 text-sm text-slate-500">{{ point.description }}</p>
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
          class="group rounded-2xl border border-slate-200 bg-white p-6 text-center shadow-sm transition-all hover:-translate-y-1 hover:border-primary-200 hover:shadow-lg"
        >
          <span class="mx-auto inline-flex h-12 w-12 items-center justify-center rounded-xl bg-primary-100 ring-1 ring-primary-200">
            <component :is="icons[stat.icon]" class="h-6 w-6 text-primary-700" />
          </span>
          <p class="mt-4 font-heading text-3xl font-extrabold text-slate-900 sm:text-4xl">{{ stat.value }}</p>
          <p class="mt-1 text-sm font-medium text-slate-500">{{ stat.label }}</p>
        </div>
      </div>
    </div>
  </section>
</template>
