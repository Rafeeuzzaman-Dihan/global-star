<script setup lang="ts">
import site from '~/data/site.json'

useSeoMeta({
  title: `Products — ${site.brand.name}`,
  description: 'Browse our range of networking products including routers, ONUs, CCTV equipment and accessories.',
})
</script>

<template>
  <div class="pt-20">
    <ProductsSection />
  </div>
</template>
