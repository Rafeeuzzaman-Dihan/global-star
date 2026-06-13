<script setup lang="ts">
import { ref, computed } from 'vue'
import { CheckIcon, BoltIcon } from '@heroicons/vue/24/outline'
import packagesData from '~/data/packages.json'

const activeTab = ref(packagesData.tabs[0]!.id)
const filteredPackages = computed(() =>
  packagesData.packages.filter((pkg) => pkg.category === activeTab.value),
)
</script>

<template>
  <section id="packages" class="bg-surface-muted py-16 sm:py-20 lg:py-24">
    <div class="mx-auto max-w-7xl px-4 sm:px-6 lg:px-8">
      <SectionHeading :kicker="packagesData.kicker" :heading="packagesData.heading" :subtitle="packagesData.subtitle" />

      <!-- Tab switcher -->
      <div class="mt-10 flex justify-center">
        <div class="inline-flex rounded-2xl border border-slate-200 bg-white p-1.5 shadow-sm">
          <button
            v-for="tab in packagesData.tabs"
            :key="tab.id"
            type="button"
            class="rounded-xl px-6 py-2.5 text-sm font-semibold transition-all sm:px-9"
            :class="activeTab === tab.id
              ? 'bg-primary-600 text-white shadow-md shadow-primary-300/40'
              : 'text-slate-500 hover:text-slate-800'"
            @click="activeTab = tab.id"
          >{{ tab.label }}</button>
        </div>
      </div>

      <!-- Package cards -->
      <div class="mt-12 grid gap-6 sm:grid-cols-2 lg:grid-cols-4">
        <article
          v-for="pkg in filteredPackages"
          :key="pkg.name"
          class="relative flex flex-col rounded-2xl p-7 transition-all duration-300 hover:-translate-y-1.5"
          :class="pkg.popular
            ? 'bg-gradient-to-b from-primary-600 to-primary-900 shadow-2xl shadow-primary-300/30 ring-2 ring-primary-500/50 hover:shadow-primary-400/40'
            : 'border border-slate-200 bg-white shadow-sm hover:border-primary-200 hover:shadow-lg'"
        >
          <!-- Popular badge -->
          <span
            v-if="pkg.popular"
            class="absolute -top-3.5 left-1/2 -translate-x-1/2 rounded-full bg-gradient-to-r from-orange-500 to-amber-400 px-4 py-1 text-xs font-bold uppercase tracking-wide text-white shadow-lg"
          >Most Popular</span>

          <!-- Speed badge -->
          <span
            class="inline-flex items-center gap-1.5 self-start rounded-full px-3 py-1 text-xs font-bold"
            :class="pkg.popular ? 'bg-white/15 text-white' : 'bg-primary-100 text-primary-700'"
          >
            <BoltIcon class="h-3.5 w-3.5" />
            {{ pkg.speed }}
          </span>

          <h3 class="mt-4 text-xl font-bold" :class="pkg.popular ? 'text-white' : 'text-slate-900'">{{ pkg.name }}</h3>

          <p class="mt-2 flex items-baseline gap-1">
            <span class="font-heading text-3xl font-extrabold" :class="pkg.popular ? 'text-white' : 'text-slate-900'">
              {{ pkg.price }}
            </span>
            <span class="text-sm" :class="pkg.popular ? 'text-primary-200' : 'text-slate-400'">{{ pkg.period }}</span>
          </p>

          <!-- Divider -->
          <div class="my-5 h-px w-full" :class="pkg.popular ? 'bg-white/15' : 'bg-slate-100'" />

          <ul class="flex-1 space-y-3">
            <li
              v-for="feature in pkg.features"
              :key="feature"
              class="flex items-start gap-2.5 text-sm"
              :class="pkg.popular ? 'text-primary-100' : 'text-slate-500'"
            >
              <CheckIcon class="mt-0.5 h-4 w-4 shrink-0" :class="pkg.popular ? 'text-primary-300' : 'text-primary-600'" />
              {{ feature }}
            </li>
          </ul>

          <a
            href="#contact"
            class="mt-7 rounded-xl px-5 py-3 text-center text-sm font-bold transition-all"
            :class="pkg.popular
              ? 'bg-white text-primary-700 hover:bg-primary-50 shadow-lg'
              : 'bg-primary-600 text-white hover:bg-primary-700 shadow-sm shadow-primary-200'"
          >{{ pkg.cta }}</a>
        </article>
      </div>

      <!-- Shared features strip -->
      <div class="mt-10 rounded-2xl border border-slate-200 bg-white px-6 py-5 shadow-sm">
        <div class="flex flex-col items-center gap-3 text-center lg:flex-row lg:justify-center lg:gap-3">
          <span class="flex items-center gap-2 text-sm font-bold text-slate-700">
            <CheckIcon class="h-4 w-4 text-primary-600" />
            {{ packagesData.sharedFeatures.label }}
          </span>
          <ul class="flex flex-wrap items-center justify-center gap-x-5 gap-y-2">
            <li
              v-for="item in packagesData.sharedFeatures.items"
              :key="item"
              class="flex items-center gap-1.5 text-sm text-slate-500"
            >
              <span class="h-1.5 w-1.5 rounded-full bg-primary-500" />
              {{ item }}
            </li>
          </ul>
        </div>
      </div>
    </div>
  </section>
</template>
