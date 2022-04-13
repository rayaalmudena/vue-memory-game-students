<script setup>

// Importamos el JSON. Vue ya lo convierte en un array de objetos y lo poe en la variable pokedex 
import pokedex from './assets/pokedex.json';
import Card from './components/Card.vue';
import backCardImage from './assets/back-card.png';
let pokemons = pokedex.slice(0,10);
console.log(pokemons);
</script>

<template>
  <header>
    <h1>¡PokeMemory!</h1>
  </header>

  <main>
    <Card :back="backCardImage" front="/pokemons/666.png" :reveal="false"/>
    <Card :back="backCardImage" front="/pokemons/555.png" :reveal="false"/>
    <Card :back="backCardImage" front="/pokemons/777.png" :reveal="false"/>
  </main>
</template>

<style>
@import "./assets/base.css";

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
