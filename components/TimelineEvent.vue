<template>
  <div class="bg-white rounded-lg shadow-md p-6 transition-transform hover:scale-[1.02]">
    <div class="flex items-start gap-4">
      <img
        :src="event.image"
        :alt="event.title"
        class="w-24 h-16 object-cover rounded"
      />
      <div class="flex-1">
        <div class="text-sm text-gray-500 mb-1">
          {{ formatDate(event.date) }}
        </div>
        <h3 class="text-xl font-semibold mb-2">{{ event.title }}</h3>
        <p class="text-gray-600">{{ event.description }}</p>
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