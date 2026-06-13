<script setup lang="ts">
import { ClockIcon, AcademicCapIcon, RectangleStackIcon } from '@heroicons/vue/24/outline'
import courses from '~/data/courses.json'

const levelClasses: Record<string, string> = {
  Beginner:     'bg-blue-100 text-blue-700 ring-1 ring-blue-200',
  Intermediate: 'bg-amber-100 text-amber-700 ring-1 ring-amber-200',
  Advanced:     'bg-purple-100 text-purple-700 ring-1 ring-purple-200',
}
</script>

<template>
  <section id="courses" class="bg-surface-muted py-16 sm:py-20 lg:py-24">
    <div class="mx-auto max-w-7xl px-4 sm:px-6 lg:px-8">
      <SectionHeading :kicker="courses.kicker" :heading="courses.heading" :subtitle="courses.subtitle" />

      <div class="mt-12 grid gap-6 sm:grid-cols-2 lg:grid-cols-3">
        <article
          v-for="course in courses.items"
          :key="course.title"
          class="group flex flex-col overflow-hidden rounded-2xl border border-slate-200 bg-white shadow-sm transition-all duration-300 hover:-translate-y-1 hover:border-primary-200 hover:shadow-lg"
        >
          <!-- Course image area -->
          <div class="aspect-[16/9] bg-gradient-to-br from-slate-50 to-blue-50/60 p-4">
            <ImagePlaceholder :src="course.image" :label="course.imageLabel" />
          </div>

          <div class="flex flex-1 flex-col px-5 pb-6 pt-4">
            <span
              class="self-start rounded-full px-3 py-1 text-xs font-semibold"
              :class="levelClasses[course.level]"
            >{{ course.level }}</span>

            <h3 class="mt-3 text-base font-bold text-slate-900">{{ course.title }}</h3>
            <p class="mt-1.5 flex-1 text-sm leading-relaxed text-slate-500">{{ course.description }}</p>

            <!-- Meta row -->
            <ul class="mt-4 flex flex-wrap items-center gap-x-4 gap-y-2 text-xs font-medium text-slate-400">
              <li class="flex items-center gap-1.5">
                <ClockIcon class="h-3.5 w-3.5 text-primary-500" />
                {{ course.duration }}
              </li>
              <li class="flex items-center gap-1.5">
                <RectangleStackIcon class="h-3.5 w-3.5 text-primary-500" />
                {{ course.classes }}
              </li>
              <li v-if="course.certificate" class="flex items-center gap-1.5">
                <AcademicCapIcon class="h-3.5 w-3.5 text-primary-500" />
                Certificate
              </li>
            </ul>

            <div class="mt-5 flex items-center justify-between border-t border-slate-100 pt-4">
              <span class="font-heading text-lg font-extrabold text-slate-900">{{ course.price }}</span>
              <a
                href="#contact"
                class="rounded-xl bg-primary-600 px-5 py-2.5 text-xs font-bold text-white shadow-sm shadow-primary-200 transition-all hover:bg-primary-700"
              >Enroll Now</a>
            </div>
          </div>
        </article>
      </div>
    </div>
  </section>
</template>
