<script setup lang="ts">
import { ref } from 'vue';

type card = {
card1:string;
card2:string;
turned: boolean;
hidden: boolean;
set? : string
}

const animals = ["hen", "dog", "chick", "kitten", "veal", "horse"];

const cards = ref<card[]>([])

animals.map(item => cards.value.push({
  card1: item,
  card2: item,
  turned: false,
  hidden: false
}));

</script>

<template>
  <main>
<div v-for="card in cards" :key="card.card1">
  <img :src="'/img/'+ card.card1 + '.webp'" :alt="card.card1">

</div>
  </main>
</template>
