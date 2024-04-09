<template>
  <main>
    <div class="hero-image">
      <img :src="HeroImage" alt="Galaxy Hero" />
    </div>
  </main>
</template>

<script setup>
import HeroImage from '../assets/images/galaxy-hero.png'
</script>

<style scoped>
.hero-image {
  position: relative;
  width: 100%;
}

.hero-image img {
  width: 100%;
}

.hero-image::after {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
background: radial-gradient(circle at center, rgba(13, 1, 11, 0) 0%, rgba(13, 1, 11, 1) 100%);
}
</style>
