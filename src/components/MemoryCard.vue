<template>
  <div class="card">
    <img :src="'/img/' + MemoryCard.set + '.webp'" :alt="MemoryCard.set">
    <div v-if="!MemoryCard.turned" class="cover"></div>
  </div>

</template>

<script setup lang="ts">
import { defineProps } from 'vue';
import type { card } from '../views/HomeView.vue';

defineProps<{
  MemoryCard: card;
}>();
</script>
<style scoped>
.card {
  position: relative;
}
.cover {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-color: green;
}
img {
  display: block;
  max-width: 100%;
}
</style>
