<script setup lang="ts">
defineProps<{
  balance: number
}>()
</script>

<template>
  <div class="bg-purple-800 rounded-lg p-4 mb-6 text-center">
    <h2 class="text-2xl font-bold">Balance: ${{ balance }}</h2>
  </div>
</template>