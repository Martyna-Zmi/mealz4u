<script setup>
defineProps({
  toggleIngredients: Function,
  toggleInstructions: Function,
  loadRandomMeal: Function
});
const basicButtonStyle = "rounded-2xl p-3 border-1 m-3 hover:scale-105"
</script>

<template>
  <button :class="`${basicButtonStyle} bg-emerald-600 hover:bg-emerald-400 border-emerald-800`"
          @click="toggleIngredients()">
    Ingredients
  </button>

  <button :class="`${basicButtonStyle} bg-emerald-600 hover:bg-emerald-400 border-emerald-800`"
          @click="toggleInstructions()">
    Instructions
  </button>

  <button
      :class="`${basicButtonStyle} bg-amber-600 hover:bg-amber-400 border-amber-800`"
      @click="loadRandomMeal()">
    Re-roll
  </button>
</template>