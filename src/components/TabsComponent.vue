<script setup>
import AchievementsComponent from './AchievementsComponent.vue'
import { inject } from 'vue'

const gameData = inject('gameData')
</script>

<template>
  <div>
    <div class="border-b border-gray-300 dark:border-gray-700">
      <ul
        class="flex flex-wrap justify-center text-sm font-medium text-center"
        id="default-tab"
        data-tabs-toggle="#default-tab-content"
        role="tablist"
      >
        <li class="me-2" role="presentation">
          <button
            id="options-tab"
            data-tabs-target="#options"
            type="button"
            role="tab"
            aria-controls="options"
            aria-selected="false"
            class="inline-flex items-center justify-center p-4 border-b-2 rounded-t-lg"
          >
            <svg
              xmlns="http://www.w3.org/2000/svg"
              class="w-4 h-4 me-2"
              viewBox="0 0 24 24"
              stroke-width="2"
              stroke="currentColor"
              fill="none"
              stroke-linecap="round"
              stroke-linejoin="round"
            >
              <path stroke="none" d="M0 0h24v24H0z" fill="none" />
              <path
                d="M10.325 4.317c.426 -1.756 2.924 -1.756 3.35 0a1.724 1.724 0 0 0 2.573 1.066c1.543 -.94 3.31 .826 2.37 2.37a1.724 1.724 0 0 0 1.065 2.572c1.756 .426 1.756 2.924 0 3.35a1.724 1.724 0 0 0 -1.066 2.573c.94 1.543 -.826 3.31 -2.37 2.37a1.724 1.724 0 0 0 -2.572 1.065c-.426 1.756 -2.924 1.756 -3.35 0a1.724 1.724 0 0 0 -2.573 -1.066c-1.543 .94 -3.31 -.826 -2.37 -2.37a1.724 1.724 0 0 0 -1.065 -2.572c-1.756 -.426 -1.756 -2.924 0 -3.35a1.724 1.724 0 0 0 1.066 -2.573c-.94 -1.543 .826 -3.31 2.37 -2.37c1 .608 2.296 .07 2.572 -1.065z"
              />
              <path d="M9 12a3 3 0 1 0 6 0a3 3 0 0 0 -6 0" />
            </svg>
            Ajustes
          </button>
        </li>
        <li class="me-2" role="presentation">
          <button
            id="achievements-tab"
            data-tabs-target="#achievements"
            type="button"
            role="tab"
            aria-controls="achievements"
            aria-selected="false"
            class="inline-flex items-center justify-center p-4 border-b-2 rounded-t-lg"
          >
            <svg
              xmlns="http://www.w3.org/2000/svg"
              class="w-4 h-4 me-2"
              width="24"
              height="24"
              viewBox="0 0 24 24"
              stroke-width="2"
              stroke="currentColor"
              fill="none"
              stroke-linecap="round"
              stroke-linejoin="round"
            >
              <path stroke="none" d="M0 0h24v24H0z" fill="none" />
              <path d="M8 21l8 0" />
              <path d="M12 17l0 4" />
              <path d="M7 4l10 0" />
              <path d="M17 4v8a5 5 0 0 1 -10 0v-8" />
              <path d="M5 9m-2 0a2 2 0 1 0 4 0a2 2 0 1 0 -4 0" />
              <path d="M19 9m-2 0a2 2 0 1 0 4 0a2 2 0 1 0 -4 0" /></svg
            >Logros
          </button>
        </li>
      </ul>
    </div>
    <div id="default-tab-content" class="mb-2 flex justify-center">
      <div
        class="hidden p-4 rounded-lg w-full max-w-56 space-y-4"
        id="options"
        role="tabpanel"
        aria-labelledby="options-tab"
      >
        <div class="flex justify-between">
          <span class="ms-3 text-sm font-medium text-gray-900">Máximo</span>
          <label class="relative inline-flex items-center me-5 cursor-pointer">
            <input
              id="maxPoints"
              type="checkbox"
              value=""
              class="sr-only peer"
              v-model="gameData.maxPointsShown"
            />
            <div
              class="w-11 h-6 bg-gray-300 rounded-full peer peer-checked:after:translate-x-full rtl:peer-checked:after:-translate-x-full peer-checked:after:border-white after:content-[''] after:absolute after:top-0.5 after:start-[2px] after:bg-white after:border-gray-300 after:border after:rounded-full after:h-5 after:w-5 after:transition-all peer-checked:bg-green-500"
            ></div>
          </label>
        </div>
        <div class="flex justify-between">
          <span class="ms-3 text-sm font-medium text-gray-900">Total</span>
          <label class="relative inline-flex items-center me-5 cursor-pointer">
            <input
              id="total"
              type="checkbox"
              value=""
              class="sr-only peer"
              v-model="gameData.totalShown"
            />
            <div
              class="w-11 h-6 bg-gray-300 rounded-full peer peer-checked:after:translate-x-full rtl:peer-checked:after:-translate-x-full peer-checked:after:border-white after:content-[''] after:absolute after:top-0.5 after:start-[2px] after:bg-white after:border-gray-300 after:border after:rounded-full after:h-5 after:w-5 after:transition-all peer-checked:bg-green-500"
            ></div>
          </label>
        </div>
        <div class="flex justify-between">
          <span class="ms-3 text-sm font-medium text-gray-900">Reinicios</span>
          <label class="relative inline-flex items-center me-5 cursor-pointer">
            <input
              id="resets"
              type="checkbox"
              value=""
              class="sr-only peer"
              v-model="gameData.resetsShown"
            />
            <div
              class="w-11 h-6 bg-gray-300 rounded-full peer peer-checked:after:translate-x-full rtl:peer-checked:after:-translate-x-full peer-checked:after:border-white after:content-[''] after:absolute after:top-0.5 after:start-[2px] after:bg-white after:border-gray-300 after:border after:rounded-full after:h-5 after:w-5 after:transition-all peer-checked:bg-green-500"
            ></div>
          </label>
        </div>
      </div>
      <div
        class="hidden p-4 rounded-lg w-full max-w-lg max-h-lg"
        id="achievements"
        role="tabpanel"
        aria-labelledby="achievements-tab"
      >
        <AchievementsComponent />
      </div>
    </div>
  </div>
</template>
