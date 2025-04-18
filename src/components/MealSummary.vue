<script setup>
defineProps({
  randomMeal: Object
})
</script>

<template>
  <h2>{{randomMeal.strMeal}}</h2>
  <img :src="randomMeal.strMealThumb" alt={{randomMeal.strName}} width="400px" height="auto">
  <p>This dish is {{randomMeal.strArea}}</p>
</template>
