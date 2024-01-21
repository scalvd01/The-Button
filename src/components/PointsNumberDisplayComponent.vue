<script setup>
import { inject } from 'vue'

const gameData = inject('gameData')
</script>
<template>
  <div>
    <h1>
      {{ gameData.points }}
    </h1>
  </div>
</template>
