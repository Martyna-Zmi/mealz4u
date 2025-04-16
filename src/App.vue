<script setup>
import {onMounted, ref} from "vue";
import {VueSpinnerPuff} from 'vue3-spinners';
const randomMeal = ref();
const error = ref();
const loaded = ref(false);

onMounted(async () => {
  await loadRandomMeal();
  });
const loadRandomMeal = async () => {
  loaded.value = false
  await fetch('https://www.themealdb.com/api/json/v1/1/random.php', {
    method: "GET",
  })
      .then((response) => {
        response.json().then((data) => {
          randomMeal.value = data.meals[0];
          //useful fields: strMeal, strInstructions, strArea, strMealThumb, strTags
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
</script>

<template>
<div>
  <h1>Your random meal for today's dinner is...</h1>
  <div v-if="!loaded">
    <VueSpinnerPuff size="100" />
  </div>
  <div v-else>
    <p>Data loaded</p>
  </div>
</div>
</template>