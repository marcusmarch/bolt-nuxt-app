<template>
  <div class="max-w-3xl mx-auto">
    <h2 class="text-2xl font-bold mb-6">Important Events</h2>

    <div class="space-y-4" ref="timelineRef">
      <TimelineEvent v-for="event in visibleEvents" :key="event" :event="event" />
    </div>

    <div v-if="loading" class="text-center py-4">
      <div class="animate-spin rounded-full h-8 w-8 border-b-2 border-gray-900 mx-auto"></div>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue'
import { useInfiniteScroll } from '@vueuse/core'
import { timelineEvents } from '../data/timelineEvents'

const timelineRef = ref(null)
const loading = ref(false)
const page = ref(1)
const visibleEvents = ref([])

const loadMoreEvents = async () => {
  if (loading.value) return

  loading.value = true
  // Simulate API delay
  await new Promise(resolve => setTimeout(resolve, 500))

  const startIdx = (page.value - 1) * 5
  const endIdx = Math.min(startIdx + 5, timelineEvents.length)
  const newEvents = timelineEvents.slice(startIdx, endIdx)

  if (newEvents.length > 0) {
    visibleEvents.value.push(...newEvents)
    page.value++
  }

  loading.value = false
}

// Initialize with first batch
loadMoreEvents()

// Setup infinite scroll
// useInfiniteScroll(
//   timelineRef,
//   () => {
//     loadMoreEvents()
//   },
//   { distance: 10 }
// )
</script>