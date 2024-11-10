<template>
  <div class="bg-white rounded-lg shadow-md p-6 transition-transform hover:scale-[1.02]">
    <div class="flex items-start gap-4">
      <figure>
        <img :src="event.image" :alt="event.title" class="w-24 h-16 object-cover rounded">
        <figcaption>
          {{ event.imageAttribution }}
        </figcaption>
      </figure>
      <div class="flex-1">
        <div class="text-sm text-gray-500 mb-1">
          {{ formatDate(event.date) }}
        </div>
        <h3 class="text-xl font-semibold mb-2">{{ event.title }}</h3>
        <p class="text-gray-600">{{ event.description }}</p>
        <a v-if="event.link" :href="event.link" target="_blank">
          <span v-if="event.linkText">{{ event.linkText }}</span>
          <span v-else>Click Here for details</span></a>
      </div>
    </div>
  </div>
</template>

<script setup>
import { format } from 'date-fns'

const props = defineProps({
  event: {
    type: Object,
    required: true
  }
})

const formatDate = (date) => {
  return format(new Date(date), 'MMMM do, yyyy')
}
</script>

<style scoped>
figcaption {
  opacity: 0;
  transition: opacity 0.3s ease;
  position: absolute;
  bottom: 0;
  width: 100%;
  background-color: rgba(0, 0, 0, 0.7);
  color: white;
  padding: 10px;
  pointer-events: none;
}

figure:hover figcaption {
  opacity: 1;
}
</style>