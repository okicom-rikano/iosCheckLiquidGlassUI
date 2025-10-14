<script setup lang="ts">
import { ref, watch } from 'vue'
import { Dialog, DialogPanel, DialogTitle } from '@headlessui/vue'

const isOpen = ref(false)

function openModal() {
  isOpen.value = true
}

function closeModal() {
  isOpen.value = false
}

// Add/remove modal-open class on body when modal opens/closes
watch(isOpen, (newValue) => {
  if (newValue) {
    document.body.classList.add('modal-open')
  } else {
    document.body.classList.remove('modal-open')
  }
})
</script>

<template>
  <div>
    <button
      type="button"
      @click="openModal"
      class="rounded-md bg-indigo-600 px-4 py-2 text-sm font-medium text-white hover:bg-indigo-700 focus:outline-none focus-visible:ring-2 focus-visible:ring-indigo-500 focus-visible:ring-offset-2"
    >
      モーダルを開く
    </button>

    <Dialog :open="isOpen" @close="closeModal" class="relative z-50">
      <!-- Transparent overlay that closes on click -->
      <div class="fixed inset-0 bg-transparent" aria-hidden="true" @click="closeModal" />

      <!-- Full-screen container to center the panel -->
      <div class="fixed inset-0 flex items-center justify-center p-4">
        <DialogPanel class="w-full max-w-md rounded-lg bg-white p-6 shadow-xl">
          <DialogTitle class="text-lg font-medium leading-6 text-gray-900 mb-4">
            モーダルダイアログ
          </DialogTitle>

          <div class="mt-2">
            <p class="text-sm text-gray-500 mb-4">
              これはHeadless UIのDialogコンポーネントを使用したモーダルの例です。
              オーバーレイは透明で、クリックすると閉じます。
            </p>
            <p class="text-sm text-gray-500 mb-4">
              モーダルが開いている間、bodyタグに<code class="bg-gray-100 px-1 rounded">modal-open</code>クラスが付与され、
              背景が減光されます。
            </p>
            <p class="text-sm text-gray-500">
              高さの指定には100vhではなく<code class="bg-gray-100 px-1 rounded">h-dvh</code>を使用しています。
            </p>
          </div>

          <div class="mt-6 flex justify-end space-x-3">
            <button
              type="button"
              @click="closeModal"
              class="rounded-md bg-indigo-600 px-4 py-2 text-sm font-medium text-white hover:bg-indigo-700 focus:outline-none focus-visible:ring-2 focus-visible:ring-indigo-500 focus-visible:ring-offset-2"
            >
              閉じる
            </button>
          </div>
        </DialogPanel>
      </div>
    </Dialog>
  </div>
</template>
