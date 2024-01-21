<script setup>
import LogoComponent from './LogoComponent.vue'
import PointsNumberDisplayComponent from './PointsNumberDisplayComponent.vue'
import MenuComponent from './MenuComponent.vue'
</script>

<template>
  <header class="flex justify-center">
    <div class="grid grid-cols-2 grow sm:mt-6 sm:mx-8 m-4 max-w-screen-md">
      <LogoComponent class="text-nowrap order-1 z-10 pl-3" />

      <PointsNumberDisplayComponent
        class="text-4xl font-bold order-3 flex justify-center content-center col-span-2"
      />

      <MenuComponent class="order-2 flex justify-end" />
    </div>
  </header>
</template>



