<script setup>
defineProps({
  isShowingIngredients: Boolean,
  randomMeal: Object
})
</script>

<template>
  <div v-if="isShowingIngredients" class="w-1/2">
    <div v-for="index in 20" :key="index">
      <p>{{randomMeal[`strIngredient${index}`]}} {{randomMeal[`strMeasure${index}`]}}</p>
    </div>
  </div>
</template>