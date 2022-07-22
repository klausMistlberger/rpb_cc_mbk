<script setup>
import { ref } from 'vue';
import Header from './components/Header.vue';
import Slider from './components/Slider.vue';
import './assets/main.css';

const dataUrl = 'https://zoo-animal-api.herokuapp.com/animals/rand/5';
const animals = [];
const dataLoaded = ref(false);
const fetchError = ref(false);
const errorMessage = ref('Loading data...');
const counter = ref(0);

const fetchData = async () => {
  const response = await fetch(dataUrl);
  if (response && response.ok) {
    const data = await response.json();
    data.forEach((element, index) => animals.push({ ...element, ix: index }));
    dataLoaded.value = true;
  } else {
    throw new Error('Something went wrong...');
  }
};

const fetchDataErrorBoundaries = async () => {
  fetchError.value = false;
  errorMessage.value = null;
  try {
    await fetchData();
  } catch (error) {
    fetchError.value = true;
    errorMessage.value = error.message;
  }
};

const clickHandler = () => {
  fetchDataErrorBoundaries();
  counter.value++;
  console.log(counter.value);
};

fetchDataErrorBoundaries();
</script>

<template>
  <Header />
  <Slider v-if="dataLoaded" :data="animals" />
  <div v-else>
    <div v-if="counter < 5">
      <div class="message-container" v-if="!fetchError">
        <div class="message">Loading data...</div>
      </div>
      <div class="message-container" v-else>
        <div class="message">{{ errorMessage }}</div>
        <button class="tryagain" @click="clickHandler">Try again</button>
      </div>
    </div>
    <div v-else>
      <div class="message--container">
        <div class="message unavailable">
          <p>Service currently unavailable.</p>
          <p>Please try again later.</p>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
.message-container {
  display: flex;
  flex-direction: column;
}

.message {
  margin: 16px;
  text-align: center;
}

.tryagain {
  width: 180px;
  margin: 0 auto;
}

.unavailable {
  color: purple;
}
</style>
