<script setup lang="ts">
import { ref, computed } from 'vue'
import { ShoppingCartIcon } from '@heroicons/vue/24/outline'
import products from '~/data/products.json'

const activeCategory = ref(products.categories[0]!)
const filteredProducts = computed(() =>
  activeCategory.value === 'All'
    ? products.items
    : products.items.filter((item) => item.category === activeCategory.value),
)
</script>

<template>
  <section id="products" class="bg-surface py-16 sm:py-20 lg:py-24">
    <div class="mx-auto max-w-7xl px-4 sm:px-6 lg:px-8">
      <SectionHeading :kicker="products.kicker" :heading="products.heading" :subtitle="products.subtitle" />

      <!-- Category filter chips -->
      <div class="mt-10 flex flex-wrap justify-center gap-2.5">
        <button
          v-for="category in products.categories"
          :key="category"
          type="button"
          class="rounded-full px-5 py-2 text-sm font-semibold transition-all"
          :class="activeCategory === category
            ? 'bg-primary-600 text-white shadow-lg shadow-primary-900/40'
            : 'bg-surface-card text-ink-muted ring-1 ring-white/10 hover:text-white hover:ring-primary-500/40'"
          @click="activeCategory = category"
        >{{ category }}</button>
      </div>

      <!-- Product cards -->
      <div class="mt-12 grid gap-5 sm:grid-cols-2 lg:grid-cols-4">
        <article
          v-for="product in filteredProducts"
          :key="product.name"
          class="group flex flex-col overflow-hidden rounded-2xl bg-surface-card ring-1 ring-white/10 transition-all duration-300 hover:-translate-y-1.5 hover:ring-primary-500/40 hover:shadow-xl hover:shadow-primary-950/60"
        >
          <!-- Product image placeholder.
               REPLACE ImagePlaceholder with <img :src="product.image" ... /> when assets exist in public/images/products/. -->
          <div class="aspect-[4/3] p-3">
            <ImagePlaceholder :src="product.image" :label="product.imageLabel" />
          </div>

          <div class="flex flex-1 flex-col px-5 pb-6 pt-1">
            <span class="self-start rounded-full bg-primary-500/15 px-3 py-1 text-xs font-semibold text-primary-400">
              {{ product.category }}
            </span>
            <h3 class="mt-3 text-base font-bold text-white">{{ product.name }}</h3>
            <p class="mt-1.5 flex-1 text-sm text-ink-muted">{{ product.description }}</p>
            <div class="mt-4 flex items-center justify-between">
              <span class="font-heading text-lg font-extrabold text-white">{{ product.price }}</span>
              <a
                href="#contact"
                class="inline-flex items-center gap-1.5 rounded-xl bg-primary-500/15 px-4 py-2 text-xs font-semibold text-primary-400 ring-1 ring-primary-500/25 transition-all hover:bg-primary-600 hover:text-white hover:ring-primary-500"
              >
                <ShoppingCartIcon class="h-4 w-4" />
                Order Now
              </a>
            </div>
          </div>
        </article>
      </div>
    </div>
  </section>
</template>
