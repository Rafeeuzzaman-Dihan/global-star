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

      <!-- Category filter -->
      <div class="mt-10 flex flex-wrap justify-center gap-2.5">
        <button
          v-for="category in products.categories"
          :key="category"
          type="button"
          class="rounded-full px-5 py-2 text-sm font-semibold transition-all"
          :class="activeCategory === category
            ? 'bg-primary-600 text-white shadow-md shadow-primary-300/30'
            : 'border border-slate-200 bg-white text-slate-500 hover:border-primary-200 hover:text-primary-700 hover:bg-primary-50'"
          @click="activeCategory = category"
        >{{ category }}</button>
      </div>

      <!-- Product cards -->
      <div class="mt-12 grid gap-5 sm:grid-cols-2 lg:grid-cols-4">
        <article
          v-for="product in filteredProducts"
          :key="product.name"
          class="group flex flex-col overflow-hidden rounded-2xl border border-slate-200 bg-white shadow-sm transition-all duration-300 hover:-translate-y-1 hover:border-primary-200 hover:shadow-lg"
        >
          <!-- Product image area -->
          <div class="aspect-[4/3] bg-gradient-to-br from-slate-50 to-blue-50/60 p-4">
            <ImagePlaceholder :src="product.image" :label="product.imageLabel" />
          </div>

          <div class="flex flex-1 flex-col px-5 pb-6 pt-4">
            <span class="self-start rounded-full bg-primary-100 px-3 py-1 text-xs font-semibold text-primary-700">
              {{ product.category }}
            </span>
            <h3 class="mt-3 text-base font-bold text-slate-900">{{ product.name }}</h3>
            <p class="mt-1.5 flex-1 text-sm leading-relaxed text-slate-500">{{ product.description }}</p>
            <div class="mt-5 flex items-center justify-between border-t border-slate-100 pt-4">
              <span class="font-heading text-lg font-extrabold text-slate-900">{{ product.price }}</span>
              <a
                href="#contact"
                class="inline-flex items-center gap-1.5 rounded-xl bg-primary-600 px-4 py-2 text-xs font-semibold text-white shadow-sm shadow-primary-200 transition-all hover:bg-primary-700"
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
