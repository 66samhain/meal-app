<script setup>
import { computed, ref } from '@vue/reactivity';
import axiosClient from '../axiosClient';
import store from '../store'
import { useRoute } from 'vue-router';
import { onMounted } from 'vue';

const route = useRoute()
const keyword = ref('')
const meals = computed(() => store.state.searchedMeals)

function searchMeals() {
  store.dispatch('searchMeals', keyword.value)
}

onMounted(() => {
  keyword.value = route.params.name

  if (keyword.value) {
    searchMeals()
  }
})
</script>

<template>
  <div class="p-8 pb-0">
    <input 
      v-model="keyword"
      type="text" 
      class="rounded border-2 border-gray-200 w-full" 
      placeholder="Search for meals" 
      @change="searchMeals">
  </div>

  <div class="grid grid-cols-1 md:grid-cols-3 gap-5 p-8">
    <div v-for="meal of meals" :key="meal.idMeal" class="bg-white shadow rounded-xl">
      <router-link to="/">
        <img 
          :src="meal.strMealThumb" 
          :alt="meal.strMeal" 
          class="rounded-t-xl h-48 w-full object-cover">
      </router-link>

      <div class="p-3">
        <h3 class="font-bold">{{ meal.strMeal }}</h3>
        <p class="mb-4">Lorem ipsum dolor sit amet, consectetur adipiscing elit. Mauris aliquam imperdiet odio, id ornare metus tempus ac. Sed vehicula, leo sit amet tristique auctor, tellus dolor tincidunt nisi, sollicitudin viverra turpis tellus ac purus. Quisque sed pulvinar mi. </p>
        <div class="flex items-center justify-between">
          <a :href="meal.strYoutube" target="_blank" 
            class="px-3 py-2 rounded border border-2 text-white border-red-600 bg-red-500 hover:bg-red-600 transition-colors">YouTube</a>
          <!-- <router-link to="/" class="px-3 py-2 rounded border border-2 text-white border-purple-600 bg-purple-500 hover:bg-purple-600 transition-colors">
            View
          </router-link> -->
        </div>
      </div>
    </div>
  </div>
</template>