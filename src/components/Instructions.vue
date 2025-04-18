<script setup>
defineProps({
  isShowingInstructions: Boolean,
  steps: Array
})
</script>

<template>
  <div v-if="isShowingInstructions" class="w-1/2">
    <div v-if="steps.length > 1" v-for="(step, index) in steps" :key="index">
      <p class="p-1">Step {{index+1}}) {{ step }}</p>
    </div>
    <div v-else v-for="(step, index) in steps" :key="index+20">
      <p>{{ step }}</p>
    </div>
  </div>
</template>
