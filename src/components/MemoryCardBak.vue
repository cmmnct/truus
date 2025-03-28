<template>
  <div class="card" @click="flipCard">
    <div :class="{ flipped: isFlipped }">
      <div class="card-front">
        <img :src="imageSrc" :alt="name" />
      </div>
      <div class="card-back">
        <p>Cover</p>
      </div>
    </div>
  </div>
</template>

<script lang="ts">

export default {
  name: "MemoryCard",
  props: {
    name: {
      type: String,
      required: true,
    },
    imageSrc: {
      type: String,
      required: true,
    },
  },
  data() {
    return {
      isFlipped: false,
    };
  },
  methods: {
    flipCard() {
      this.isFlipped = !this.isFlipped;
    },
  },
};
</script>

<style scoped>
.card {
  width: 100px;
  height: 150px;
  perspective: 1000px;
  cursor: pointer;
}
.card > div {
  width: 100%;
  height: 100%;
  position: relative;
  transform-style: preserve-3d;
  transition: transform 0.6s;
}
.card > div.flipped {
  transform: rotateY(180deg);
}
.card-front,
.card-back {
  width: 100%;
  height: 100%;
  position: absolute;
  backface-visibility: hidden;
}
.card-front {
  transform: rotateY(180deg);
}
.card-back {
  display: flex;
  align-items: center;
  justify-content: center;
  background-color: #ccc;
  color: #000;
}
</style>
