<script setup lang="ts">
import { ref, watch } from 'vue'

const props = defineProps<{
  spinning: boolean
}>()

const emits = defineEmits<{
  (e: 'spin', bet: number): void
}>()

const symbols = ['🍒', '🍊', '🍇', '💎', '7️⃣', '🎰']
const reels = ref([
  symbols[Math.floor(Math.random() * symbols.length)],
  symbols[Math.floor(Math.random() * symbols.length)],
  symbols[Math.floor(Math.random() * symbols.length)]
])
const bet = ref(10)

watch(() => props.spinning, (spinning) => {
  if (spinning) {
    const interval = setInterval(() => {
      reels.value = reels.value.map(() => symbols[Math.floor(Math.random() * symbols.length)])
    }, 100)
    setTimeout(() => clearInterval(interval), 2000)
  }
})

const handleSpin = () => {
  emits('spin', bet.value)
}
</script>

<template>
  <div class="bg-purple-800 rounded-lg p-6 shadow-xl">
    <div class="flex justify-center gap-4 mb-6 text-6xl bg-purple-700 p-4 rounded">
      <div v-for="(symbol, index) in reels" :key="index" 
           class="w-24 h-24 flex items-center justify-center bg-purple-600 rounded">
        {{ symbol }}
      </div>
    </div>
    <div class="flex items-center justify-between gap-4 mb-4">
      <label class="text-lg">Bet Amount:</label>
      <select v-model="bet" class="bg-purple-700 p-2 rounded">
        <option :value="10">10</option>
        <option :value="20">20</option>
        <option :value="50">50</option>
        <option :value="100">100</option>
      </select>
    </div>
    <button @click="handleSpin" 
            :disabled="spinning"
            class="w-full bg-yellow-500 hover:bg-yellow-600 disabled:bg-gray-500 
                   text-black font-bold py-3 px-6 rounded-lg transition">
      {{ spinning ? 'Spinning...' : 'SPIN!' }}
    </button>
  </div>
</template>