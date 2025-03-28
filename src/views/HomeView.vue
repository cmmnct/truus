<script setup lang="ts">
import { ref } from 'vue';

type card = {
  set: string;
  turned: boolean;
  hidden: boolean;
  card1?: string;
  card2?: string;
}

const customers = [
  {
    name: "Alice Smith",
    function: "Designer",
  },
  {
    name: "Bob Johnson",
    function: "Project Manager",
  },
  {
    name: "Charlie Brown",
    function: "QA Engineer",
  },
  {
    name: "Diana Prince",
    function: "Frontend Developer",
  },
  {
    name: "Ethan Hunt",
    function: "Backend Developer",
  },
  {
    name: "Fiona Gallagher",
    function: "DevOps Engineer",
  }
];

const animals = ["hen", "dog", "chick", "kitten", "veal", "horse"];

const cards = ref<card[]>([])

animals.map(item => cards.value.push(
  {
  set: item,
  turned: false,
  hidden: false
}
));

</script>

<template>
  <main>
    <div v-for="card in cards" :key="card.set">
      <img :src="'/img/' + card.set + '.webp'" :alt="card.set">

    </div>
  </main>
</template>
