<template>
    <div class="flex flex-col min-h-screen">
        <Header/>
        <main class="flex-1">
             <slot/>
        </main>
        <footer class="w-100 px-6 py-4 flex font-light justify-center border-t border-gray-200 "><span>feito com ❤️ por Joaquim Jambo</span></footer>
    </div>
</template>


