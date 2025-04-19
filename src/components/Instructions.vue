<script setup>
defineProps({
  isShowingInstructions: Boolean,
  steps: Array
})
</script>

<template>
  <div v-if="isShowingInstructions" class="m-2 w-1/4 bg-green-200 p-4 outline outline-4 outline-green-50 border-4 border-green-100 rounded-lg">
    <h3 class="font-semibold">Instructions</h3>
    <div v-if="steps.length > 1" v-for="(step, index) in steps" :key="index">
      <p class="p-1">Step {{index+1}}) {{ step }}</p>
    </div>
    <div v-else v-for="(step, index) in steps" :key="index+20">
      <p>{{ step }}</p>
    </div>
  </div>
</template>
