<script setup>
import { computed } from '@vue/reactivity';
import { ref } from 'vue';
import { onMounted } from 'vue';
import axiosClient from '../axiosClient.js'

const letters = 'ABCDEFGHIJKLMNOPQRSTUVWXYZ'.split('')
const ingredients = ref([])

onMounted(async () => {
  const response = await axiosClient.get('list.php?c=list')
  ingredients.value = response.data
})
</script>

<template>
  <div class="flex flex-col p-8">
    <div class="flex justify-center gap-2 mt-2">
      <router-link :to="{name: 'byLetter', params: {letter}}" v-for="letter in letters" :key="letter">
        {{ letter }}
      </router-link>
    </div>
  </div>  
</template>