<script setup>
import { inject } from 'vue'

const gameData = inject('gameData')
</script>

<template>
  <div class="flex flex-col items-center text-2xl font-semibold">
    <h1 v-if="gameData.maxPointsShown">Máximo: {{ gameData.maxPoints }}</h1>
    <h1 v-if="gameData.totalShown">Total: {{ gameData.total }}</h1>
    <h1 v-if="gameData.resetsShown">Reinicios: {{ gameData.resets }}</h1>
  </div>
</template>
