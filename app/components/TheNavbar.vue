<script setup lang="ts">
import { ref, onMounted, onUnmounted } from 'vue'
import { StarIcon, Bars3Icon, XMarkIcon } from '@heroicons/vue/24/solid'
import site from '~/data/site.json'

const { brand, nav } = site
const mobileOpen = ref(false)
const scrolled    = ref(false)

const onScroll = () => { scrolled.value = window.scrollY > 12 }

onMounted(() => {
  window.addEventListener('scroll', onScroll, { passive: true })
  onScroll()
})
onUnmounted(() => window.removeEventListener('scroll', onScroll))
const close = () => { mobileOpen.value = false }
</script>

<template>
  <header
    class="fixed inset-x-0 top-0 z-50 transition-all duration-300"
    :class="scrolled
      ? 'bg-surface/80 shadow-lg shadow-black/30 backdrop-blur-xl border-b border-white/[0.06]'
      : 'bg-transparent'"
  >
    <nav class="mx-auto flex h-16 max-w-7xl items-center justify-between px-4 sm:px-6 lg:h-20 lg:px-8" aria-label="Main">

      <!-- Logo -->
      <a href="#home" class="flex items-center gap-2.5 group" @click="close">
        <span class="flex h-9 w-9 items-center justify-center rounded-xl bg-gradient-to-br from-primary-500 to-primary-700 shadow-lg shadow-primary-900/50 transition-shadow group-hover:shadow-primary-600/60">
          <StarIcon class="h-5 w-5 text-white" />
        </span>
        <span class="font-heading text-lg font-bold text-white">{{ brand.name }}</span>
      </a>

      <!-- Desktop links -->
      <ul class="hidden items-center gap-7 lg:flex">
        <li v-for="link in nav.links" :key="link.label">
          <a :href="link.href" class="text-sm font-medium text-ink-muted transition-colors hover:text-white">
            {{ link.label }}
          </a>
        </li>
      </ul>

      <!-- Desktop CTA -->
      <a
        :href="nav.cta.href"
        class="hidden rounded-xl bg-primary-600 px-5 py-2.5 text-sm font-semibold text-white shadow-lg shadow-primary-900/40 transition-all hover:bg-primary-500 hover:shadow-primary-600/50 lg:inline-block"
      >{{ nav.cta.label }}</a>

      <!-- Hamburger -->
      <button
        type="button"
        class="rounded-lg p-2 text-ink-muted hover:bg-white/10 hover:text-white lg:hidden transition-colors"
        :aria-expanded="mobileOpen"
        aria-label="Toggle menu"
        @click="mobileOpen = !mobileOpen"
      >
        <Bars3Icon v-if="!mobileOpen" class="h-6 w-6" />
        <XMarkIcon v-else class="h-6 w-6" />
      </button>
    </nav>

    <!-- Mobile menu -->
    <Transition
      enter-active-class="transition duration-200 ease-out"
      enter-from-class="-translate-y-2 opacity-0"
      enter-to-class="translate-y-0 opacity-100"
      leave-active-class="transition duration-150 ease-in"
      leave-from-class="translate-y-0 opacity-100"
      leave-to-class="-translate-y-2 opacity-0"
    >
      <div v-if="mobileOpen" class="border-t border-white/[0.07] bg-surface-muted/95 backdrop-blur-xl shadow-xl lg:hidden">
        <ul class="space-y-1 px-4 py-4">
          <li v-for="link in nav.links" :key="link.label">
            <a
              :href="link.href"
              class="block rounded-xl px-4 py-2.5 text-sm font-medium text-ink-muted transition-colors hover:bg-white/8 hover:text-white"
              @click="close"
            >{{ link.label }}</a>
          </li>
          <li class="pt-2">
            <a
              :href="nav.cta.href"
              class="block rounded-xl bg-primary-600 px-4 py-3 text-center text-sm font-semibold text-white hover:bg-primary-500"
              @click="close"
            >{{ nav.cta.label }}</a>
          </li>
        </ul>
      </div>
    </Transition>
  </header>
</template>
