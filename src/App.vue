<script setup>
import { ref } from 'vue';

import Header from './components/Header.vue';
import Slider from './components/Slider.vue';

import './assets/main.css';

const dataUrl = 'https://zoo-animal-api.herokuapp.com/animals/rand/5';
const animals = [];
const dataLoaded = ref(false);

const fetchData = async () => {
  const response = await fetch(dataUrl);
  const data = await response.json();
  data.forEach((element, index) => animals.push({ ...element, ix: index }));
  dataLoaded.value = true;
};
fetchData();
</script>

<template>
  <Header />
  <Slider v-if="dataLoaded" :data="animals" />
  <div v-else class="loading">Loading data...</div>
</template>

<style scoped>
.loading {
  margin: 1em;
  text-align: center;
}
</style>
