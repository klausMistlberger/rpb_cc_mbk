<script setup>
import { ref } from 'vue';

const props = defineProps({
  data: Object,
  length: Number,
});

const name = ref(props.data.name);
const weight = ref(props.data.weight_max);
const image = ref(props.data.image_link);
const nameLabel = `Tier ${props.data.ix + 1} von ${props.length}`;

name.value.length <= 18
  ? (name.value = name.value)
  : (name.value = name.value.slice(0, 15) + '...');

document.querySelectorAll('.card--a').forEach((el) => {
  el.addEventListener('click', (event) => {
    event.preventDefault();
  });
});
</script>

<template>
  <li :aria-labelledby="nameLabel">
    <a href="#" class="card--anchor">
      <div class="card--container">
        <div class="image--container">
          <img class="card--image" :src="image" />
        </div>
        <div class="card--info">
          <span class="card--info-name">{{ name }}</span>
          <span class="card--info-upto legend">bis zu</span>
          <span class="card--info-weight">{{ weight }}</span>
          <span class="card--info-unit legend">kg</span>
        </div>
      </div>
    </a>
  </li>
</template>

<style>
:root {
  --radius: 15px;
}

.card--anchor {
  text-decoration: none;
}

.card--container {
  width: 285px;
  height: 220px;
  box-shadow: -2px 2px var(--yellow);
  border-radius: var(--radius);
}

.image--container {
  width: 100%;
  height: 80%;
  overflow: hidden;
}

.card--image {
  width: 100%;
  display: block;
  margin: auto;
  border-top-left-radius: calc(var(--radius) + 3px);
  border-top-right-radius: calc(var(--radius) + 3px);
}

.card--info {
  height: 20%;
  display: flex;
  align-items: baseline;
  gap: 3px;
  margin: 0 16px;
}

.card--info > * {
  margin: 12px 0;
  color: var(--magenta);
}

.card--info-name {
  font-weight: 700;
  color: var(--green);
}

.card--info-upto {
  margin-left: auto;
}

.card--info-weight {
  font-weight: 600;
}

.legend {
  font-size: 12px;
}
</style>
