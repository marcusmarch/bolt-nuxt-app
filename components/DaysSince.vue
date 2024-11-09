<template>
  <div class="container mx-auto px-4 py-8">
    <h1 class="text-6xl font-bold text-red-600 text-center mb-8">
      Days Since Trump Became A Dictator
    </h1>
    <div class="text-center mb-12">
      <div class="text-4xl font-bold">
        {{ daysCount }} days
      </div>
      <div v-if="startDate" class="text-xl text-gray-600">
        since {{ formatDate(startDate) }}
      </div>
      <div v-else class="text-xl text-gray-600 italic">
        Hasn't happened yet but will start counting as soon as it does
      </div>
    </div>

    <Timeline />
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue'
import { format, differenceInDays } from 'date-fns'

const startDate = null;// new Date(Date.now()) // uncomment when he becomes a dictator ;)
const daysCount = ref(0)

const updateDaysCount = () => {
  if (startDate) {
    daysCount.value = differenceInDays(new Date(), startDate)
  }
}

const formatDate = (date) => {
  return format(date, 'MMMM do, yyyy')
}

onMounted(() => {
  updateDaysCount()
  //setInterval(updateDaysCount, 1000 * 60) // Update every minute
})
</script>