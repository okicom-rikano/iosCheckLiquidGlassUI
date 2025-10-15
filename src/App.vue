<script setup lang="ts">
import { ref } from 'vue'
import ModalExample from './components/ModalExample.vue'

const height = ref('h-dvh');
</script>

<template>
  <div class="overflow-scroll flex items-start justify-center bg-gradient-to-br from-blue-50 to-indigo-100 border-b-4 border-red-500 p-4" :class="height">
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

      <div>
        <textarea id="story" name="story" rows="20" class="mt-4 w-full p-2 border border-gray-300 rounded-md focus:outline-none focus:ring-2 focus:ring-blue-500" placeholder="ここにテキストを入力してください...">
          親譲りの無鉄砲で小供の時から損ばかりしている。小学校に居る時分学校の二階から飛び降りて一週間ほど腰を抜かした事がある。なぜそんな無闇をしたと聞く人があるかも知れぬ。別段深い理由でもない。新築の二階から首を出していたら、同級生の一人が冗談に、いくら威張っても、そこから飛び降りる事は出来まい。弱虫やーい。と囃したからである。小使に負ぶさって帰って来た時、おやじが大きな眼をして二階ぐらいから飛び降りて腰を抜かす奴があるかと云ったから、この次は抜かさずに飛んで見せますと答えた。（青空文庫より）
        </textarea>
      </div>
    </div>
  </div>
</template>
