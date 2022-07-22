<script async setup>
import Card from './Card.vue';

const props = defineProps({
  data: Array,
});
</script>

<template>
  <section role="region">
    <div class="slider--nav">
      <a href="#" role="link" class="slider--theme"><h2>Zootiere</h2></a>
      <a
        href="https://www.restplatzboerse.at/"
        target="_blank"
        class="slider--all"
        role="link"
        >Alle</a
      >
    </div>
    <h3 aria-labelledby="">Zufällige Auswahl an Zootieren</h3>

    <div class="slide--container">
      <ul>
        <Card
          v-for="animal in props.data"
          :key="animal.id"
          :data="animal"
          :length="props.data.length"
        />
      </ul>
      <div class="overlay"></div>
    </div>
  </section>
</template>

<style scoped>
section {
  margin: 1em;
  position: relative;
}

h2 {
  font-family: 'Quicksand', sans-serif;
  font-weight: 700;
  font-size: 24px;
  color: var(--green);
}

h3 {
  color: var(--grey);
  font-size: 16px;
  font-weight: 400;
}

.slider--nav {
  display: flex;
  justify-content: space-between;
  align-items: baseline;
}

.slider--theme {
  text-decoration: none;
}

.slider--all {
  text-decoration: none;
  color: var(--green);
}

.slide--container {
  position: relative;
}

ul {
  padding: 1em 0;
  display: flex;
  flex-wrap: nowrap;
  gap: 16px;

  overflow-x: scroll;
  overflow-y: hidden;
  scrollbar-width: none;
}

ul::-webkit-scrollbar {
  display: none;
}

li {
  list-style: none;
  /* flex: 1 1 16rem; */
}

.overlay {
  position: absolute;
  margin: 1em 0;
  height: calc(100% - 2em + 2px);
  width: 23px;
  top: 0;
  right: 0;
  background-image: linear-gradient(to left, #ffffff, #ffffff00);
}
</style>
