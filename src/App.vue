<script setup lang="ts">
import { ref } from 'vue'
import ModalExample from './components/ModalExample.vue'

const height = ref('h-dvh');
</script>

<template>
  <div class="flex items-center justify-center bg-gradient-to-br from-blue-50 to-indigo-100 border-b-4 border-red-500 p-4" :class="height">
    <div class="text-center">
      <h1 class="text-4xl font-bold text-gray-800 mb-8">
        Vue 3 + Vite + TypeScript + Tailwind
      </h1>
      <div class="mb-3">
        <p>Current height class: {{ height }}</p>
      </div>
      <div class="flex space-x-1 mb-3">
        <!-- change height  -->
        <button type="button" class="bg-blue-500 text-white px-4 py-2 font-xs rounded-md" @click="height = 'h-dvh'">h-dvh</button>
        <button type="button" class="bg-blue-600 text-white px-4 py-2 font-xs rounded-md" @click="height = 'h-screen'">h-screen(100vh)</button>
        <button type="button" class="bg-blue-700 text-white px-4 py-2 font-xs rounded-md" @click="height = 'h-lvh'">h-lvh(100lvh)</button>
      </div>
      <ModalExample />
    </div>
  </div>
</template>
