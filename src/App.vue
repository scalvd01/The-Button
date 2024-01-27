<script setup>
import HeaderComponent from './components/HeaderComponent.vue'
import TheButtonComponent from './components/TheButtonComponent.vue'
import StatsInfoComponent from './components/StatsInfoComponent.vue'
import { onMounted, ref, provide, computed, watch } from 'vue'
import { initFlowbite, Modal } from 'flowbite'
import { watchOnce } from '@vueuse/core'
import { Toaster, toast } from 'vue-sonner'

function loadFromStorage() {
  const data = localStorage.getItem('gameData')
  if (data) {
    gameData.value = JSON.parse(atob(data))
  } else {
    console.log('No se pudieron cargar los datos')
  }

  const achievements = localStorage.getItem('achievements')
  if (achievements) {
    const a = JSON.parse(atob(achievements))

    a.forEach((element) => {
      if (element.isUnlocked) {
        achievementsList.value.find((achievement) => achievement.id === element.id).isUnlocked =
          true
      }
    })
  } else {
    console.log('No se pudieron cargar los logros')
  }
}

function saveToStorage() {
  localStorage.setItem('gameData', btoa(JSON.stringify(gameData.value)))
  localStorage.setItem('achievements', btoa(JSON.stringify(achievementsList.value)))
}

let modalTutorial = null
function showTutorial() {
  const tutorial = localStorage.getItem('tutorial')
  if (!tutorial) {
    const $targetEl = document.querySelector('#popup-modal')

    const options = {
      placement: 'center-center',
      backdrop: 'dynamic',
      backdropClasses: 'bg-white/10 backdrop-blur-sm fixed inset-0 z-40',
      closable: true
    }

    // instance options object
    const instanceOptions = {
      id: 'popup-modal',
      override: true
    }

    modalTutorial = new Modal($targetEl, options, instanceOptions)
    modalTutorial.show()
  }
}

onMounted(() => {
  initFlowbite()
  loadFromStorage()
  achievementsList.value.forEach((achievement) => {
    if (!achievement.isUnlocked) {
      watchOnce(
        computed(() => achievement.trigger()),
        () => {
          toast.success(achievement.title, {
            description: achievement.description
          })
          achievement.isUnlocked = true
        }
      )
    }
  })

  watch(gameData.value, () => {
    saveToStorage()
  })

  showTutorial()
})

const gameData = ref({
  points: 0,
  prevResetPoints: 101,
  maxPoints: 0,
  total: 0,
  resets: 0,
  currentProb: 0,
  maxPointsShown: true,
  totalShown: true,
  resetsShown: true
})
provide('gameData', gameData)

const achievementsList = ref([
  {
    id: 1,
    title: 'Solo estamos empezando.',
    description: 'Consigue 5 puntos.',
    isUnlocked: false,
    color: 'red',
    number: '5',
    trigger() {
      return gameData.value.points >= 5
    }
  },
  {
    id: 2,
    title: 'La mayoría llegan aquí.',
    description: 'Consigue 10 puntos.',
    isUnlocked: false,
    color: 'red',
    number: '10',
    trigger() {
      return gameData.value.points >= 10
    }
  },
  {
    id: 3,
    title: 'No te rindas ahora.',
    description: 'Consigue 15 puntos.',
    isUnlocked: false,
    color: 'red',
    number: '15',
    trigger() {
      return gameData.value.points >= 15
    }
  },
  {
    id: 4,
    title: 'Esto es más dificil de lo que parece.',
    description: 'Consigue 20 puntos.',
    isUnlocked: false,
    color: 'red',
    number: '20',
    trigger() {
      return gameData.value.points >= 20
    }
  },
  {
    id: 5,
    title: 'No te flipes.',
    description: 'Consigue 25 puntos.',
    isUnlocked: false,
    color: 'red',
    number: '25',
    trigger() {
      return gameData.value.points >= 25
    }
  },
  {
    id: 6,
    title: 'Es tu día de suerte.',
    description: 'Consigue 30 puntos.',
    isUnlocked: false,
    color: 'red',
    number: '30',
    trigger() {
      return gameData.value.points >= 30
    }
  },
  {
    id: 7,
    title: 'No te preocupes, le puede pasar a cualquiera.',
    description: 'Reinicia tu puntuación por debajo de los 5 puntos.',
    isUnlocked: false,
    color: 'blue',
    number: '5',
    trigger() {
      return gameData.value.prevResetPoints < 5
    }
  },
  {
    id: 8,
    title: '¿Te ha mirado un tuerto?',
    description: 'Reinicia tu puntuación por debajo de los 3 puntos.',
    isUnlocked: false,
    color: 'blue',
    number: '3',
    trigger() {
      return gameData.value.prevResetPoints < 3
    }
  },
  {
    id: 9,
    title: 'Es normal.',
    description: 'Reinicia tu puntuación 5 veces.',
    isUnlocked: false,
    color: 'orange',
    number: '5',
    trigger() {
      return gameData.value.resets >= 5
    }
  },
  {
    id: 10,
    title: 'No desesperes.',
    description: 'Reinicia tu puntuación 20 veces.',
    isUnlocked: false,
    color: 'orange',
    number: '20',
    trigger() {
      return gameData.value.resets >= 20
    }
  },
  {
    id: 11,
    title: 'Sigue intentándolo.',
    description: 'Reinicia tu puntuación 50 veces.',
    isUnlocked: false,
    color: 'orange',
    number: '50',
    trigger() {
      return gameData.value.resets >= 50
    }
  },
  {
    id: 12,
    title: 'Es solo el principio.',
    description: 'Pulsa el botón 20 veces.',
    isUnlocked: false,
    color: 'green',
    number: '20',
    trigger() {
      return gameData.value.total >= 20
    }
  },
  {
    id: 13,
    title: 'Seguimos aumentando',
    description: 'Pulsa el botón 100 veces.',
    isUnlocked: false,
    color: 'green',
    number: '100',
    trigger() {
      return gameData.value.total >= 100
    }
  },
  {
    id: 14,
    title: '¿Qué te impide seguir?',
    description: 'Pulsa el botón 500 veces.',
    isUnlocked: false,
    color: 'green',
    number: '500',
    trigger() {
      return gameData.value.total >= 500
    }
  }
])
provide('achievementsList', achievementsList)

function setTutorialToWatched() {
  localStorage.setItem('tutorial', 'true')
  modalTutorial.hide()
}
</script>

<template>
  <Toaster position="bottom-center" richColors />
  <HeaderComponent />
  <main class="flex flex-col items-center">
    <StatsInfoComponent />

    <!-- <TheButtonComponent class="absolute bottom-1/2 translate-y-1/2 size-52" /> -->
    <TheButtonComponent class="mt-24 size-52" />
  </main>

  <div
    id="popup-modal"
    tabindex="-1"
    aria-hidden="true"
    class="fixed left-0 right-0 top-0 z-50 hidden h-[calc(100%-1rem)] max-h-full w-full overflow-y-auto overflow-x-hidden p-4 md:inset-0"
  >
    <div class="relative max-h-full w-full max-w-2xl">
      <!-- Modal content -->
      <div class="relative rounded-lg bg-[#fef9db] shadow-xl shadow-gray-500/80">
        <!-- Modal header -->
        <div
          class="flex items-center justify-center p-4 md:p-5 border-b rounded-t dark:border-gray-600"
        >
          <h1 class="text-3xl font-bold">THE BUTTON</h1>
        </div>
        <!-- Modal body -->
        <div class="p-4 md:p-5">
          <h3 class="mb-5 text-lg font-normal text-gray-500 dark:text-gray-400">
            Cada vez que pulsas el botón ganas 1 punto.
            <br />
            Cada vez que pulsas el botón las probabilidades de perder todos tus puntos aumentan en
            un 1%.
            <br />
            Consigue todos los logros y la puntuación más alta posible.
            <br />
            <br />
            Buena suerte.
          </h3>
          <div class="flex justify-center">
            <button
              @click="setTutorialToWatched()"
              type="button"
              class="text-white bg-green-500 hover:bg-green-700 focus:ring-4 focus:outline-none font-medium rounded-lg text-sm inline-flex items-center px-5 py-2.5 text-center me-2"
            >
              Entendido
            </button>
          </div>
        </div>
        <!-- Modal footer -->
      </div>
    </div>
  </div>
</template>

<style scoped></style>
