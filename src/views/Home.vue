<script setup>
import { computed } from '@vue/reactivity';
import store from '../store';

const meals = computed(() => store.state.meals)
</script>

<template>
  <pre>{{ meals }}</pre>
</template>