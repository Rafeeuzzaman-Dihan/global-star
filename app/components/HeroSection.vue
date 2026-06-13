<script setup lang="ts">
import { ref, onMounted, onUnmounted } from 'vue'
import type { Component } from 'vue'
import { ShieldCheckIcon, ClockIcon, BoltIcon } from '@heroicons/vue/24/outline'
import { ChevronRightIcon, ChevronLeftIcon } from '@heroicons/vue/20/solid'
import site from '~/data/site.json'

const { hero } = site
const icons: Record<string, Component> = { ShieldCheckIcon, ClockIcon, BoltIcon }

const slides = [
  { src: '/hero-1.jpg', alt: 'Fast Fiber Internet Connection' },
  { src: '/hero-2.jpg', alt: 'Enterprise IT Solutions' },
  { src: '/hero-3.jpg', alt: 'Professional IT Training' },
]

const stats = [
  { value: '5K+', label: 'Subscribers' },
  { value: '99.9%', label: 'Uptime' },
  { value: '1 Hr', label: 'Installation' },
]

const activeSlide = ref(0)
let timer: ReturnType<typeof setInterval> | null = null

function setSlide(i: number) {
  activeSlide.value = i
  if (timer) clearInterval(timer)
  timer = setInterval(() => {
    activeSlide.value = (activeSlide.value + 1) % slides.length
  }, 4500)
}

const prevSlide = () => setSlide((activeSlide.value - 1 + slides.length) % slides.length)
const nextSlide = () => setSlide((activeSlide.value + 1) % slides.length)

onMounted(() => {
  timer = setInterval(() => {
    activeSlide.value = (activeSlide.value + 1) % slides.length
  }, 4500)
})

onUnmounted(() => {
  if (timer) clearInterval(timer)
})
</script>

<template>
  <section id="home" class="bg-[#080d1a]">

    <!-- ── PART 1: Pure full-width image slider (zero text on top) ── -->
    <div class="relative mt-16 h-[62vh] min-h-[380px] w-full overflow-hidden lg:mt-20">

      <template v-for="(slide, i) in slides" :key="slide.src">
        <Transition name="hero-fade">
          <div v-if="activeSlide === i" class="absolute inset-0">
            <img :src="slide.src" :alt="slide.alt" class="h-full w-full object-cover object-center" />
          </div>
        </Transition>
      </template>

      <!-- Soft bottom fade so slider merges into the content below -->
      <div class="pointer-events-none absolute inset-x-0 bottom-0 h-28 bg-gradient-to-t from-[#080d1a] to-transparent" />

      <!-- Prev / Next arrows -->
      <button
        type="button"
        class="absolute left-3 top-1/2 z-10 -translate-y-1/2 rounded-full border border-white/20 bg-black/30 p-2.5 text-white backdrop-blur-sm transition hover:bg-black/60 sm:left-5"
        aria-label="Previous slide"
        @click="prevSlide"
      >
        <ChevronLeftIcon class="h-5 w-5" />
      </button>
      <button
        type="button"
        class="absolute right-3 top-1/2 z-10 -translate-y-1/2 rounded-full border border-white/20 bg-black/30 p-2.5 text-white backdrop-blur-sm transition hover:bg-black/60 sm:right-5"
        aria-label="Next slide"
        @click="nextSlide"
      >
        <ChevronRightIcon class="h-5 w-5" />
      </button>

      <!-- Dot navigation -->
      <div class="absolute bottom-6 left-1/2 z-10 flex -translate-x-1/2 gap-2">
        <button
          v-for="(_, i) in slides"
          :key="i"
          type="button"
          class="h-1.5 rounded-full transition-all duration-300"
          :class="activeSlide === i ? 'w-8 bg-primary-400' : 'w-1.5 bg-white/40 hover:bg-white/70'"
          :aria-label="`Go to slide ${i + 1}`"
          @click="setSlide(i)"
        />
      </div>
    </div>

    <!-- ── PART 2: Hero content — clean on dark background ─────── -->
    <div class="mx-auto max-w-7xl px-4 pb-16 pt-10 sm:px-6 lg:px-8">

      <!-- Badge -->
      <div class="flex justify-center lg:justify-start">
        <span class="inline-flex items-center gap-2 rounded-full bg-primary-500/10 px-4 py-2 text-xs font-bold uppercase tracking-widest text-primary-400 ring-1 ring-primary-500/30">
          <BoltIcon class="h-3.5 w-3.5" />
          {{ hero.badge }}
        </span>
      </div>

      <!-- Heading -->
      <h1 class="mt-5 text-center text-3xl font-extrabold leading-tight tracking-tight text-white sm:text-4xl lg:text-left lg:text-5xl">
        {{ hero.headline }}
      </h1>

      <p class="mx-auto mt-4 max-w-2xl text-center text-base leading-relaxed text-slate-400 sm:text-lg lg:mx-0 lg:text-left">
        {{ hero.subtext }}
      </p>

      <!-- CTAs + stats -->
      <div class="mt-8 flex flex-col items-center gap-8 lg:flex-row lg:items-center lg:justify-between">
        <div class="flex flex-wrap justify-center gap-3 lg:justify-start">
          <a
            :href="hero.primaryCta.href"
            class="inline-flex items-center gap-2 rounded-xl bg-primary-600 px-7 py-3.5 text-sm font-semibold text-white shadow-lg shadow-primary-900/40 transition-all hover:bg-primary-500"
          >
            {{ hero.primaryCta.label }}
            <ChevronRightIcon class="h-4 w-4" />
          </a>
          <a
            :href="hero.secondaryCta.href"
            class="inline-flex items-center justify-center rounded-xl px-7 py-3.5 text-sm font-semibold text-white ring-1 ring-white/20 transition-all hover:bg-white/10"
          >
            {{ hero.secondaryCta.label }}
          </a>
        </div>

        <!-- Vertical divider (desktop) -->
        <div class="hidden h-10 w-px shrink-0 bg-white/10 lg:block" />

        <!-- Stats -->
        <div class="flex gap-10">
          <div v-for="stat in stats" :key="stat.label" class="text-center">
            <p class="font-heading text-2xl font-extrabold text-primary-400">{{ stat.value }}</p>
            <p class="mt-0.5 text-xs font-medium text-slate-500">{{ stat.label }}</p>
          </div>
        </div>
      </div>

      <!-- Trust strip -->
      <ul class="mt-8 flex flex-wrap justify-center gap-x-8 gap-y-3 border-t border-white/[0.07] pt-6 lg:justify-start">
        <li
          v-for="item in hero.trustStrip"
          :key="item.label"
          class="flex items-center gap-2 text-sm font-medium text-slate-400"
        >
          <component :is="icons[item.icon]" class="h-4 w-4 shrink-0 text-primary-400" />
          {{ item.label }}
        </li>
      </ul>

    </div>

  </section>
</template>

<style scoped>
.hero-fade-enter-active,
.hero-fade-leave-active {
  transition: opacity 0.9s ease;
}
.hero-fade-enter-from,
.hero-fade-leave-to {
  opacity: 0;
}
</style>
