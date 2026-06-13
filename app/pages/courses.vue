<script setup lang="ts">
import site from '~/data/site.json'

useSeoMeta({
  title: `Courses — ${site.brand.name}`,
  description: 'Professional IT training courses in networking, CCTV, and more.',
})
</script>

<template>
  <div class="pt-20">
    <CoursesSection />
  </div>
</template>
