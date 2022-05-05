<template>
  <main>
    <TheHeading :level="1"> TV Finder</TheHeading>
    <MyShows :level="1">
      <template #sc="{shows}">
        <h3 v-if="shows?.length > 0">
            Avarage score: {{computedAvarage(shows).toFixed(2)}}
        </h3>
      </template>
    </MyShows>

  </main>
</template>

<script setup>
import TheHeading from './components/TheHeading.vue'
import MyShows from './components/MyShows.vue'

const computedAvarage = shows => shows.reduce((acc, info) => +info.score + acc, 0) / shows.length;
</script>

<style>
@import './assets/base.css';

#app {
  max-width: 1280px;
  margin: 0 auto;
  padding: 2rem;

  font-weight: normal;
}

header {
  line-height: 1.5;
}

.logo {
  display: block;
  margin: 0 auto 2rem;
}

a,
.green {
  text-decoration: none;
  color: hsla(160, 100%, 37%, 1);
  transition: 0.4s;
}

@media (hover: hover) {
  a:hover {
    background-color: hsla(160, 100%, 37%, 0.2);
  }
}

@media (min-width: 1024px) {
  body {
    display: flex;
    place-items: center;
  }

  #app {
    display: grid;
    grid-template-columns: 1fr 1fr;
    padding: 0 2rem;
  }

  header {
    display: flex;
    place-items: center;
    padding-right: calc(var(--section-gap) / 2);
  }

  header .wrapper {
    display: flex;
    place-items: flex-start;
    flex-wrap: wrap;
  }

  .logo {
    margin: 0 2rem 0 0;
  }
}
</style>
