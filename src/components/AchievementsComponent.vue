<script setup>
import { inject } from 'vue'

const achievementsList = inject('achievementsList')


</script>

<template>
  <div class="grid grid-cols-3 gap-4 sm:grid-cols-4 md:grid-cols-5">
    <div v-for="item in achievementsList" :key="item.id" class="flex justify-center aspect-square">
      <div
        class="rounded-full flex justify-center items-center aspect-square"
        :class="[item.isUnlocked ? `bg-${item.color}-500` : 'bg-gray-300']"
        :data-popover-target="`popover-hover-${item.id}`"
        data-popover-trigger="hover"
      >
        <span class="text-white/70 text-5xl font-semibold select-none">{{item.isUnlocked ? item.number: '?' }}</span>
      </div>
      <div
        data-popover
        :id="`popover-hover-${item.id}`"
        role="tooltip"
        class="absolute z-10 invisible inline-block w-64 text-sm text-gray-500 transition-opacity duration-300 bg-white border border-gray-200 rounded-lg shadow-sm opacity-0 dark:text-gray-400 dark:border-gray-600 dark:bg-gray-800"
      >
        <div
          class="px-3 py-2 bg-gray-100 border-b border-gray-200 rounded-t-lg dark:border-gray-600 dark:bg-gray-700"
        >
          <h3 class="font-semibold text-gray-900 dark:text-white">{{ item.title }}</h3>
        </div>
        <div class="px-3 py-2">
          <p>{{ item.description }}</p>
        </div>
        <div data-popper-arrow></div>
      </div>
    </div>
  </div>
  <div class="bg-orange-500"></div>
  <div class="bg-blue-500"></div>
</template>
