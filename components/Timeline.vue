<template>
  <div class="max-w-3xl mx-auto">
    <h2 class="text-2xl font-bold mb-6">Important Events</h2>
    
    <div class="space-y-4" ref="timelineRef">
      <TimelineEvent
        v-for="event in visibleEvents"
        :key="event.id"
        :event="event"
      />
    </div>

    <div v-if="loading" class="text-center py-4">
      <div class="animate-spin rounded-full h-8 w-8 border-b-2 border-gray-900 mx-auto"></div>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue'
import { useInfiniteScroll } from '@vueuse/core'

const timelineRef = ref(null)
const loading = ref(false)
const page = ref(1)
const visibleEvents = ref([])

// Simulated events data - in a real app, this would come from an API
const generateEvents = (page, limit = 10) => {
  return Array.from({ length: limit }, (_, i) => ({
    id: page * limit + i,
    date: new Date(Date.now() - (Math.random() * 90) * 24 * 60 * 60 * 1000),
    title: `Event ${page * limit + i + 1}`,
    description: `This is a description for event ${page * limit + i + 1}. Something important happened here.`,
    image: `https://picsum.photos/seed/${page * limit + i}/200/100`
  }))
}

const loadMoreEvents = async () => {
  if (loading.value) return
  
  loading.value = true
  // Simulate API delay
  await new Promise(resolve => setTimeout(resolve, 500))
  
  const newEvents = generateEvents(page.value)
  visibleEvents.value.push(...newEvents)
  page.value++
  
  loading.value = false
}

// Initialize with first batch
loadMoreEvents()

// Setup infinite scroll
useInfiniteScroll(
  timelineRef,
  () => {
    loadMoreEvents()
  },
  { distance: 10 }
)
</script>