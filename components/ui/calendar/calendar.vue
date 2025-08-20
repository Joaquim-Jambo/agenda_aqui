<script setup lang="ts">
import { ref, watch } from "vue"
import { CalendarDate, getLocalTimeZone, fromDate } from "@internationalized/date"

defineProps<{
  modelValue: any
}>()

const emit = defineEmits(["update:modelValue"])

const selected = ref(fromDate(new Date(), getLocalTimeZone()))

watch(selected, (val) => {
  emit("update:modelValue", val)
})
</script>

<template>
  <div class="p-2">
    <!-- Usando radix-vue para ter o calendário -->
    <DatePicker v-model="selected" class="w-full rounded-md border shadow-sm" />
  </div>
</template>
