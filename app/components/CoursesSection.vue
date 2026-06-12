<script setup lang="ts">
import { ClockIcon, AcademicCapIcon, RectangleStackIcon } from '@heroicons/vue/24/outline'
import courses from '~/data/courses.json'

const levelClasses: Record<string, string> = {
  Beginner:     'bg-primary-500/15 text-primary-400 ring-primary-500/25',
  Intermediate: 'bg-accent-500/15 text-accent-400 ring-accent-500/25',
  Advanced:     'bg-purple-500/15 text-purple-400 ring-purple-500/25',
}
</script>

<template>
  <section id="courses" class="bg-surface-muted py-16 sm:py-20 lg:py-24">
    <div class="mx-auto max-w-7xl px-4 sm:px-6 lg:px-8">
      <SectionHeading :kicker="courses.kicker" :heading="courses.heading" :subtitle="courses.subtitle" />

      <div class="mt-12 grid gap-5 sm:grid-cols-2 lg:grid-cols-3">
        <article
          v-for="course in courses.items"
          :key="course.title"
          class="group flex flex-col overflow-hidden rounded-2xl bg-surface-card ring-1 ring-white/10 transition-all duration-300 hover:-translate-y-1.5 hover:ring-primary-500/40 hover:shadow-xl hover:shadow-primary-950/60"
        >
          <!-- Course image placeholder.
               REPLACE ImagePlaceholder with <img :src="course.image" ... /> when assets exist in public/images/courses/. -->
          <div class="aspect-[16/9] p-3">
            <ImagePlaceholder :src="course.image" :label="course.imageLabel" />
          </div>

          <div class="flex flex-1 flex-col px-5 pb-6 pt-2">
            <span
              class="self-start rounded-full px-3 py-1 text-xs font-semibold ring-1"
              :class="levelClasses[course.level]"
            >{{ course.level }}</span>

            <h3 class="mt-3 text-base font-bold text-white">{{ course.title }}</h3>
            <p class="mt-1.5 flex-1 text-sm leading-relaxed text-ink-muted">{{ course.description }}</p>

            <!-- Meta row -->
            <ul class="mt-4 flex flex-wrap items-center gap-x-4 gap-y-2 text-xs font-medium text-ink-muted">
              <li class="flex items-center gap-1.5">
                <ClockIcon class="h-3.5 w-3.5 text-primary-400" />
                {{ course.duration }}
              </li>
              <li class="flex items-center gap-1.5">
                <RectangleStackIcon class="h-3.5 w-3.5 text-primary-400" />
                {{ course.classes }}
              </li>
              <li v-if="course.certificate" class="flex items-center gap-1.5">
                <AcademicCapIcon class="h-3.5 w-3.5 text-primary-400" />
                Certificate
              </li>
            </ul>

            <div class="mt-5 flex items-center justify-between border-t border-white/8 pt-4">
              <span class="font-heading text-lg font-extrabold text-white">{{ course.price }}</span>
              <a
                href="#contact"
                class="rounded-xl bg-primary-600 px-5 py-2.5 text-xs font-semibold text-white shadow-md shadow-primary-900/40 transition-all hover:bg-primary-500"
              >Enroll Now</a>
            </div>
          </div>
        </article>
      </div>
    </div>
  </section>
</template>
