<script setup>
    const props = defineProps({
        service:{
            type: String,
            required: true,
        },
        description:{
            type: String,
            required: true,
        },
        price:{
            type: Number,
            required: true,
        },
        duration:{
            type: Number,
            required: true
        }
    })
     const formatDuration = computed(()=>{
        const hour = Math.floor(props.duration / 60);
        const min = props.duration % 60;
        if (props.duration < 60) {
            return `${props.duration}min`
        }
        return min > 0 ? `${hour}h ${min}min` : `${hour}h`
  })
</script>
<template>
    <div class=" bg-white flex flex-col transition duration-200 space-y-1 p-6 shadow-sm rounded-xl hover:transition-shadow hover:shadow-md active:border-blue-600">
        <span class="font-semibold"> {{ service }} </span>
        <p class="text-gray-500 text-sm">{{ description }}</p>
        <div class="flex justify-between">
            <span class="text-blue-600 font-semibold"> {{ formatDuration }}</span>
            <span class="text-black font-bold">{{ new Intl.NumberFormat('pt-AO', { style: 'currency', currency: 'AOA' }).format(price) }}</span>
        </div>
    </div>
</template>