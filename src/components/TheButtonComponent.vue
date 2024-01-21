<script setup>
import { inject } from 'vue'

const gameData = inject('gameData')

function theButtonClicked() {
  const prob = Math.random() * 100
  if (gameData.value.currentProb < prob) {
    gameData.value.points++
    gameData.value.currentProb++
    gameData.value.total++
    if (gameData.value.points > gameData.value.maxPoints) {
      gameData.value.maxPoints = gameData.value.points
    }
  } else {
    gameData.value.prevResetPoints = gameData.value.points
    gameData.value.currentProb = 0
    gameData.value.resets++
    gameData.value.points = 0
  }
}
</script>

<template>
  <button
    @click="theButtonClicked()"
    class="bg-red-500 rounded-full transition duration-75 ease-in-out active:scale-95"
  ></button>
</template>
