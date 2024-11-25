<script setup lang="ts">
import { ref } from 'vue'
import SlotMachine from './components/SlotMachine.vue'
import Wallet from './components/Wallet.vue'

const balance = ref(1000)
const spinning = ref(false)

const handleSpin = (bet: number) => {
  if (balance.value >= bet && !spinning.value) {
    balance.value -= bet
    spinning.value = true
    setTimeout(() => {
      const win = Math.random() < 0.4
      if (win) {
        balance.value += bet * 2
      }
      spinning.value = false
    }, 2000)
  }
}
</script>

<template>
  <div class="min-h-screen bg-gradient-to-b from-purple-900 to-purple-600 text-white p-8">
    <h1 class="text-4xl font-bold text-center mb-8">Vue Casino</h1>
    <div class="max-w-2xl mx-auto">
      <Wallet :balance="balance" />
      <SlotMachine :spinning="spinning" @spin="handleSpin" />
    </div>
  </div>
</template>