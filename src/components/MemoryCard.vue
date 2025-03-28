<template>
  <img :src="'/img/' + card.set + '.webp'" :alt="card.set">
</template>

<script setup lang="ts">
import { defineProps } from 'vue';

defineProps<{
  card: {
    set: string;
    turned: boolean;
    hidden: boolean;
    card1?: string;
    card2?: string;
  }
}>();
</script>
<style scoped>

</style>
