<script setup>
import TabsComponent from './TabsComponent.vue'
import { Modal } from 'flowbite'
import { onMounted } from 'vue'

let modal = null
onMounted(() => {
  
  const $targetEl = document.querySelector('#modalEl')

  const options = {
    placement: 'center-center',
    backdrop: 'dynamic',
    backdropClasses: 'bg-white/10 backdrop-blur-sm fixed inset-0 z-40',
    closable: true
    // onHide: () => {
    //   console.log('modal is hidden')
    // },
    // onShow: () => {
    //   console.log('modal is shown')
    // },
    // onToggle: () => {
    //   console.log('modal has been toggled')
    // }
  }

  // instance options object
  const instanceOptions = {
    id: 'modalEl',
    override: true
  }

  modal = new Modal($targetEl, options, instanceOptions)
  // modal.show()
})
</script>

<template>
  <div>
    <!-- Modal toggle -->
    <button
      type="button"
      @click="modal.toggle()"
      class="relative inline-flex items-center rounded p-2 group"
    >
      <svg
        xmlns="http://www.w3.org/2000/svg"
        class="size-6 group-hover:animate-spin"
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
      <!-- <div v-if="isInfoPingActive" class="">
        <span
          class="absolute inline-flex items-center justify-center size-3 text-xs font-bold text-white bg-green-500 rounded-full top-1 end-1 animate-ping"
        ></span>
        <span
          class="absolute inline-flex items-center justify-center size-3 text-xs font-bold text-white bg-green-500 rounded-full top-1 end-1"
        ></span>
      </div> -->
    </button>

    <!-- Modal -->
    
    <div
      id="modalEl"
      tabindex="-1"
      aria-hidden="true"
      class="fixed left-0 right-0 top-0 z-50 hidden h-[calc(100%-1rem)] max-h-full w-full overflow-y-auto overflow-x-hidden p-4 md:inset-0"
    >
      <div class="relative max-h-full w-full max-w-2xl">
        <!-- Modal content -->
        <div class="relative rounded-lg bg-[#fef9db] shadow-xl shadow-gray-500/80">
          <!-- Modal header -->
          <div class="flex items-start justify-between rounded-t p-5 pb-2">
            <button
              type="button"
              @click="modal.toggle()"
              class="ms-auto inline-flex h-8 w-8 items-center justify-center rounded-lg bg-transparent text-sm text-gray-400 hover:bg-gray-200 hover:text-gray-900 dark:hover:bg-gray-600 dark:hover:text-white"
            >
              <svg
                class="h-3 w-3"
                aria-hidden="true"
                xmlns="http://www.w3.org/2000/svg"
                fill="none"
                viewBox="0 0 14 14"
              >
                <path
                  stroke="currentColor"
                  stroke-linecap="round"
                  stroke-linejoin="round"
                  stroke-width="2"
                  d="m1 1 6 6m0 0 6 6M7 7l6-6M7 7l-6 6"
                />
              </svg>
              <span class="sr-only">Close modal</span>
            </button>
          </div>
          <!-- Modal body -->
            <TabsComponent class="pb-2" />

          <!-- Modal footer -->
        </div>
      </div>
    </div>
  </div>
</template>
