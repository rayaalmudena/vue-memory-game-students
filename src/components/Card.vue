<!-- Card Component -->

<script setup>
const props = defineProps({
    back: String, //img
    front: String, //img
    reveal: Boolean
});
</script>

<template>
  <div>
    <img v-if="!reveal" :src="back" alt="pokemon card backcard" />
    <img v-else :src="front" alt="pokemonRandom" />
  </div>
</template>

<style scoped>
img {
    width: clamp(69px, 18vw, 175px);
}
</style>