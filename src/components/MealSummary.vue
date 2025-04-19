<script setup>
defineProps({
  randomMeal: Object
})
</script>

<template>
  <h2 class="text-2xl font-bold pulse-grow">{{randomMeal.strMeal}}</h2>
  <div class="flex justify-center p-2">
    <img :src="randomMeal.strMealThumb" alt={{randomMeal.strName}} width="400px" height="auto" class="rounded-2xl">
  </div>
  <p class="font-semibold">This dish is {{randomMeal.strArea}}</p>
</template>
