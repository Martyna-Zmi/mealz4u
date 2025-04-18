<script setup>
import {computed, onMounted, ref} from "vue";
import {VueSpinnerPuff} from 'vue3-spinners';
const randomMeal = ref();
const tagsArray = computed(() => {
  if(randomMeal.value && randomMeal.value.strTags){
    return randomMeal.value.strTags.split(",");
  }
})
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
  <div v-else-if="randomMeal">
    <h2>{{randomMeal.strMeal}}</h2>
    <img :src="randomMeal.strMealThumb" alt={{randomMeal.strName}} width="400px" height="auto">
    <p>This dish is {{randomMeal.strArea}}</p>
    <div v-if="tagsArray && tagsArray.length > 0">
      <p>Tags:</p>
      <div class="flex flex-row flex-wrap">
        <div v-for="tag in tagsArray">
          <button class="rounded-2xl rounded-bl-none bg-green-600 p-3 border-1 border-black m-3">{{tag}}</button>
        </div>
      </div>
    </div>
  </div>
</div>
</template>