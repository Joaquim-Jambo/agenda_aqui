<!-- components/BookingCalendar.vue -->
<script setup>
import { ref, onMounted } from 'vue'

const selectedDate = ref(null)
const selectedTime = ref(null)

const today = new Date()
const currentMonth = ref(today.getMonth())
const currentYear = ref(today.getFullYear())

const calendarDays = ref([])

function generateCalendar() {
  const firstDay = new Date(currentYear.value, currentMonth.value, 1).getDay()
  const daysInMonth = new Date(currentYear.value, currentMonth.value + 1, 0).getDate()
  
  const days = []

  // Espaços vazios antes do mês
  for (let i = 0; i < firstDay; i++) {
    days.push({ day: null })
  }

  // Dias do mês
  for (let day = 1; day <= daysInMonth; day++) {
    const isToday = day === today.getDate() && currentMonth.value === today.getMonth()
    const isPast = currentYear.value === today.getFullYear() &&
                   currentMonth.value === today.getMonth() &&
                   day < today.getDate()

    days.push({
      day,
      isToday,
      isPast
    })
  }

  calendarDays.value = days
}

const availableTimes = ['09:00','10:00','11:00','14:00','15:00','16:00','17:00']

onMounted(() => {
  generateCalendar()
})

function selectDay(day) {
  if (!day || day.isPast) return
  selectedDate.value = `${day.day}/${currentMonth.value + 1}/${currentYear.value}`
}

function selectTime(time) {
  selectedTime.value = time
}
</script>

<template>
  <div>
    <div class="mb-6 transition-all">
      <h3 class="text-sm text-gray-500 mb-3 ">Escolha a data</h3>
      
      <!-- Header da semana -->
      <div class="grid grid-cols-7 gap-1 mb-4">
        <div v-for="w in ['Dom','Seg','Ter','Qua','Qui','Sex','Sáb']"
             :key="w"
             class="text-center text-sm font-medium text-gray-500 py-2">
          {{ w }}
        </div>
      </div>
      
      <!-- Dias -->
      <div class="grid grid-cols-7 gap-1">
        <div v-for="(day, index) in calendarDays"
             :key="index"
             @click="selectDay(day)"
             class="text-center py-2 text-sm cursor-pointer rounded-lg"
             :class="[
               day.isToday ? 'bg-blue-600 text-white hover:bg-blue-700' : '',
               day.isPast ? 'text-gray-300 cursor-not-allowed' : 'hover:bg-blue-50',
               selectedDate === `${day.day}/${currentMonth+1}/${currentYear}` ? 'ring-2 ring-blue-500' : ''
             ]">
          {{ day.day }}
        </div>
      </div>
    </div>

    <!-- Slots de horário -->
    <div v-if="selectedDate" class="mt-6 p-6">
      <h3 class="font-extralight text-gray-900 mb-3">Escolha o horário</h3>
      <div class="grid grid-cols-4 gap-2" id="timeGrid">
        <button v-for="time in availableTimes"
                :key="time"
                @click="selectTime(time)"
                class="py-2 px-3 text-sm border rounded-lg"
                :class="[
                  selectedTime === time
                    ? 'bg-blue-600 text-white border-blue-600'
                    : 'border-gray-300 hover:bg-blue-50 hover:border-blue-300'
                ]">
          {{ time }}
        </button>
      </div>
    </div>
  </div>
</template>