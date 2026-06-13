<script setup lang="ts">
import type { Component } from 'vue'
import {
  RocketLaunchIcon, ChatBubbleLeftRightIcon,
  BoltIcon, BanknotesIcon, MapPinIcon,
} from '@heroicons/vue/24/outline'
import whyus from '~/data/whyus.json'

const icons: Record<string, Component> = {
  RocketLaunchIcon, ChatBubbleLeftRightIcon, BoltIcon, BanknotesIcon,
}
</script>

<template>
  <section id="why-us" class="bg-[#0b1628] py-16 sm:py-20 lg:py-24">
    <div class="mx-auto max-w-7xl px-4 sm:px-6 lg:px-8">
      <SectionHeading :kicker="whyus.kicker" :heading="whyus.heading" :subtitle="whyus.subtitle" dark />

      <div class="mt-12 grid gap-5 sm:grid-cols-2 lg:grid-cols-4">
        <article
          v-for="item in whyus.items"
          :key="item.title"
          class="group rounded-2xl bg-white/5 p-7 text-center ring-1 ring-white/10 transition-all duration-300 hover:-translate-y-1.5 hover:ring-primary-500/40 hover:bg-white/8 hover:shadow-xl hover:shadow-primary-950/60"
        >
          <span class="mx-auto inline-flex h-14 w-14 items-center justify-center rounded-2xl bg-primary-500/15 ring-1 ring-primary-500/25 transition-all group-hover:bg-primary-500/25 group-hover:ring-primary-500/50 group-hover:shadow-lg group-hover:shadow-primary-500/20">
            <component :is="icons[item.icon]" class="h-7 w-7 text-primary-400 transition-colors group-hover:text-primary-300" />
          </span>
          <h3 class="mt-5 text-base font-bold text-white">{{ item.title }}</h3>
          <p class="mt-2 text-sm leading-relaxed text-slate-400">{{ item.description }}</p>
        </article>
      </div>

      <!-- Coverage strip -->
      <div class="mt-10 flex items-center justify-center gap-3 rounded-2xl bg-white/5 px-6 py-4 ring-1 ring-white/10">
        <MapPinIcon class="h-5 w-5 shrink-0 text-primary-400" />
        <p class="text-center text-sm font-medium text-slate-400">{{ whyus.coverage }}</p>
      </div>
    </div>
  </section>
</template>
