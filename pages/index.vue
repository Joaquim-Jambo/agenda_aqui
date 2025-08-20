<script setup>
  
    const services = ref([{
    service: "Corte Feminino",
    description: "Corte personalizado com lavagem e finalização",
    duration: 50, // minutos
    price: 20000, // valor em Kz
  },
  {
    service: "Corte Masculino",
    description: "Corte clássico ou moderno, com finalização",
    duration: 40,
    price: 15000,
  },
  {
    service: "Barba Completa",
    description: "Aparar, desenhar e hidratar a barba",
    duration: 30,
    price: 10000,
  },
  {
    service: "Coloração",
    description: "Aplicação de cor permanente ou tonalizante",
    duration: 90,
    price: 35000,
  }])
 
</script>
<template>
    <div class="flex flex-col items-center p-6">
        <Banner/>
        <div class="flex flex-col w-full items-center justify-between sm:flex-row sm:justify-around ">
            <div class="flex flex-col max-w-sm space-y-2 px-2 py-4 w-full">
                <h2 class="text-2xl font-bold mb-2">Nossos Serviços</h2> 
                <div v-for="service in services" class="sm:w-[700px]">
                    <Card :service="service.service" :description="service.description" :duration="service.duration" :price="service.price"/>
                </div>        
            </div>
             <div class=" w-full max-w-md px-4 py-4 bg-white rounded-md shadow-sm ">
                <h3 class="font-bold text-2xl">Agendar Horário</h3>
                <BookingCalendar/>
            </div> 
        </div>
    </div>
</template>