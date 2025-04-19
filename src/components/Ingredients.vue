<script setup>
defineProps({
  isShowingIngredients: Boolean,
  randomMeal: Object
})
</script>

<template>
  <div v-if="isShowingIngredients" class="m-2 bg-green-200 p-4 outline outline-4 outline-green-50 border-4 border-green-100 rounded-lg">
   <h3 class="font-semibold">Ingredients</h3>
    <div v-for="index in 20" :key="index">
      <p>{{randomMeal[`strIngredient${index}`]}} {{randomMeal[`strMeasure${index}`]}}</p>
    </div>
  </div>
</template>