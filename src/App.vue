<script setup>
import { ref } from 'vue';
import Header from './components/Header.vue';
import Slider from './components/Slider.vue';
import './assets/main.css';

const dataUrl = 'https://zoo-animal-api.herokuapp.com/animals/rand/5';
const animals = [];
const dataLoaded = ref(false);
const fetchError = ref(false);

const fetchData = async () => {
  const response = await fetch(dataUrl);
  if (response && response.statusText === 'OK') {
    const data = await response.json();
    data.forEach((element, index) => animals.push({ ...element, ix: index }));
    dataLoaded.value = true;
  } else {
    throw new Error('Something went wrong...');
  }
};

const fetchDataErrorBoundaries = async () => {
  fetchError.value = false;
  try {
    await fetchData();
  } catch (error) {
    fetchError.value = true;
  }
};

fetchDataErrorBoundaries();
</script>

<template>
  <Header />
  <Slider v-if="dataLoaded" :data="animals" />
  <div v-else>
    <div class="center" v-if="!fetchError">Loading data...</div>
    <div class="message" v-else>
      <div class="center">Something went wrong...</div>
      <button class="tryagain" @click="fetchDataErrorBoundaries">
        Try again
      </button>
    </div>
  </div>
</template>

<style scoped>
.center {
  margin: 16px;
  text-align: center;
}

.message {
  display: flex;
  flex-direction: column;
}

.tryagain {
  width: 180px;
  margin: 0 auto;
}
</style>
