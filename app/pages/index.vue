<script setup lang="ts">
import site from '~/data/site.json'

useSeoMeta({
  title: `${site.brand.name} — Fast Fiber Internet & IT Solutions`,
  description: site.brand.tagline,
})
</script>

<template>
  <div>
    <HeroSection />
    <AboutSection />
    <ServicesSection />
    <PackagesSection />
    <ProductsSection />
    <CoursesSection />
    <WhyUsSection />
    <CtaSection />
  </div>
</template>
