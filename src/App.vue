<script setup>
import {computed, onMounted, ref} from "vue";
import {VueSpinnerPuff} from 'vue3-spinners';
import Tags from "./components/Tags.vue";
import Instructions from "./components/Instructions.vue";
import Ingredients from "./components/Ingredients.vue";
import MealSummary from "./components/MealSummary.vue";
import Actions from "./components/Actions.vue";

const randomMeal = ref();
const error = ref();
const loaded = ref(false);
const isShowingIngredients = ref(false);
const isShowingInstructions = ref(false);

const tagsArray = computed(() => {
  if(randomMeal.value && randomMeal.value.strTags){
    return randomMeal.value.strTags.split(",");
  }
})

const steps = computed(() => {
  if (randomMeal.value?.strInstructions) {
    return randomMeal.value.strInstructions
        .split(/\r\n\r\n/)
        .map(step => step.trim())
        .filter(step => step.length > 0);
  }
  return [];
});

onMounted(async () => {
  await loadRandomMeal();
  });

const loadRandomMeal = async () => {

  loaded.value = false
  isShowingInstructions.value = false;
  isShowingIngredients.value = false;

  await fetch('https://www.themealdb.com/api/json/v1/1/random.php', {
    method: "GET",
  })
      .then((response) => {
        response.json().then((data) => {
          randomMeal.value = data.meals[0];
        });
      })
      .catch((err) => {
            error.value = err;
          }
      )
      .finally(() => {
        loaded.value = true;
      })
}

const toggleIngredients = () => {
  isShowingIngredients.value = !isShowingIngredients.value;
  isShowingInstructions.value = false;
}
const toggleInstructions = () => {
  isShowingInstructions.value = !isShowingInstructions.value;
  isShowingIngredients.value = false;
}
</script>

<template>
    <div class="flex flex-col items-center text-center">
      <h1 class="text-xl font-bold">Mealz 4 u!</h1>
      <h2>Your random meal for today's dinner is...</h2>

      <div v-if="!loaded">
        <VueSpinnerPuff size="100"/>
      </div>

      <div v-else-if="randomMeal" class="bg-green-200 p-4 outline outline-4 outline-green-50 border-4 border-green-100 rounded-lg">
        <MealSummary :randomMeal="randomMeal"/>
        <Tags :tags-array="tagsArray"/>
        <Actions :loadRandomMeal="loadRandomMeal" :toggleIngredients="toggleIngredients" :toggleInstructions="toggleInstructions"/>
      </div>

      <Ingredients :is-showing-ingredients :random-meal="randomMeal"/>
      <Instructions :is-showing-instructions="isShowingInstructions" :steps="steps"/>
  </div>

</template>