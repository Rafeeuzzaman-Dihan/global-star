<script setup lang="ts">
import type { Component } from 'vue'
import { StarIcon } from '@heroicons/vue/24/solid'
import {
  PhoneIcon, EnvelopeIcon, MapPinIcon,
  GlobeAltIcon, PlayCircleIcon, BriefcaseIcon,
  ChatBubbleOvalLeftEllipsisIcon,
} from '@heroicons/vue/24/outline'
import site from '~/data/site.json'

const { brand, contact, social, footer } = site

// Generic stand-in icons — swap for brand SVGs when available.
const socialIcons: Record<string, Component> = {
  Facebook:  GlobeAltIcon,
  YouTube:   PlayCircleIcon,
  LinkedIn:  BriefcaseIcon,
  WhatsApp:  ChatBubbleOvalLeftEllipsisIcon,
}
</script>

<template>
  <footer id="contact" class="bg-[#0d1525] border-t border-white/[0.06]">
    <!-- Top gradient accent bar -->
    <div class="h-1 w-full bg-gradient-to-r from-primary-600 via-primary-400 to-secondary-500" />

    <div class="mx-auto max-w-7xl px-4 py-16 sm:px-6 lg:px-8">
      <div class="grid gap-10 sm:grid-cols-2 lg:grid-cols-4">

        <!-- Brand + contact -->
        <div>
          <a href="#home" class="flex items-center gap-2.5">
            <span class="flex h-9 w-9 items-center justify-center rounded-xl bg-gradient-to-br from-primary-500 to-primary-700">
              <StarIcon class="h-5 w-5 text-white" />
            </span>
            <span class="font-heading text-lg font-bold text-white">{{ brand.name }}</span>
          </a>
          <p class="mt-4 text-sm leading-relaxed text-slate-400">{{ brand.tagline }}</p>
          <ul class="mt-5 space-y-2.5 text-sm">
            <li class="flex items-center gap-2.5">
              <PhoneIcon class="h-4 w-4 shrink-0 text-primary-400" />
              <a :href="`tel:${contact.phone.replace(/\s/g, '')}`" class="text-slate-400 transition-colors hover:text-white">{{ contact.phone }}</a>
            </li>
            <li class="flex items-center gap-2.5">
              <EnvelopeIcon class="h-4 w-4 shrink-0 text-primary-400" />
              <a :href="`mailto:${contact.email}`" class="text-slate-400 transition-colors hover:text-white">{{ contact.email }}</a>
            </li>
            <li class="flex items-start gap-2.5">
              <MapPinIcon class="mt-0.5 h-4 w-4 shrink-0 text-primary-400" />
              <span class="text-slate-400">{{ contact.address }}</span>
            </li>
          </ul>
        </div>

        <!-- Quick links -->
        <nav aria-label="Quick links">
          <h3 class="text-sm font-bold uppercase tracking-wider text-white">Quick Links</h3>
          <ul class="mt-4 space-y-2.5">
            <li v-for="link in footer.quickLinks" :key="link.label">
              <a :href="link.href" class="text-sm text-slate-400 transition-colors hover:text-white">{{ link.label }}</a>
            </li>
          </ul>
        </nav>

        <!-- Services -->
        <nav aria-label="Services">
          <h3 class="text-sm font-bold uppercase tracking-wider text-white">Services</h3>
          <ul class="mt-4 space-y-2.5">
            <li v-for="link in footer.services" :key="link.label">
              <a :href="link.href" class="text-sm text-slate-400 transition-colors hover:text-white">{{ link.label }}</a>
            </li>
          </ul>
        </nav>

        <!-- Support + Social -->
        <nav aria-label="Support">
          <h3 class="text-sm font-bold uppercase tracking-wider text-white">Support</h3>
          <ul class="mt-4 space-y-2.5">
            <li v-for="link in footer.support" :key="link.label">
              <a :href="link.href" class="text-sm text-slate-400 transition-colors hover:text-white">{{ link.label }}</a>
            </li>
          </ul>
          <div class="mt-6 flex gap-2.5">
            <a
              v-for="item in social"
              :key="item.name"
              :href="item.href"
              :aria-label="item.name"
              :title="item.name"
              class="flex h-9 w-9 items-center justify-center rounded-xl bg-[#111c30] ring-1 ring-white/10 transition-all hover:bg-primary-600 hover:ring-primary-500 hover:text-white text-slate-400"
            >
              <component :is="socialIcons[item.name]" class="h-4 w-4" />
            </a>
          </div>
        </nav>
      </div>
    </div>

    <!-- Bottom bar -->
    <div class="border-t border-white/[0.06]">
      <div class="mx-auto max-w-7xl px-4 py-5 text-center text-sm sm:px-6 lg:px-8">
        <span class="text-slate-500">{{ footer.copyright }}</span>
      </div>
    </div>
  </footer>
</template>
