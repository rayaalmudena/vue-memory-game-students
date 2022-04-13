<script setup>

// Importamos el JSON. Vue ya lo convierte en un array de objetos y lo poe en la variable pokedex 
import { reactive } from 'vue';

import pokedex from './assets/pokedex.json';
import Card from './components/Card.vue';
import ChessBoard from './components/ChessBoard.vue';

import RadialProgress from "vue3-radial-progress";

import backCardImage from './assets/back-card.png';
shuffleArray(pokedex);
let pokemons = pokedex.slice(0,10);

pokemons = pokemons.map(p => ({ 
  id: p.id,
  name: p.name.english, 
  image: "/pokemons/"+p.id.toString().padStart(3,"0")+".png" 
}));

function shuffleArray(inputArray) {
    inputArray.sort(() => Math.random() - 0.5);
}
console.log(pokemons);

const state = reactive({
  score: 0,
  totalMatches: 10
})


function checkCards(isMatch) {
  if (isMatch) {
    state.score++;
  }
}

</script>

<template>
  <header>
    <h1>¡PokeMemory! </h1>
    <RadialProgress :diameter="80" :completed-steps="state.score" :total-steps="state.totalMatches">
      {{state.score}}
    </RadialProgress>
  </header>

  <main>
      <ChessBoard @onCheckedCards="checkCards" :cards="pokemons" :backCardImage="backCardImage"></ChessBoard>
  </main>
</template>

<style>
@import "./assets/base.css";

header {
  line-height: 1.5;
  display: flex;
  justify-content: space-between;
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
