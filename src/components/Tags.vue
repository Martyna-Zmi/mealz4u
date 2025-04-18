<script setup>
defineProps({
  tagsArray: Array,
})
</script>

<template>
  <div v-if="tagsArray && tagsArray.length > 0">
    <p>Tags:</p>
    <div class="flex flex-row flex-wrap justify-center">
      <div v-for="tag in tagsArray">
        <button class="rounded-2xl rounded-bl-none bg-emerald-200 p-3 border-1 border-black m-3">{{tag}}</button>
      </div>
    </div>
  </div>
</template>