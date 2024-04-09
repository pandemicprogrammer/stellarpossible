<template>
  <main>
    <div class="hero-image">
      <img :src="HeroImage" alt="Galaxy Hero" />
    </div>
  </main>
</template>

<script setup>
import HeroImage from '../assets/images/galaxy-hero.png';
</script>

<style scoped>
.hero-image {
  position: relative;
  height: 90vh; /* Set the height of the hero image to fill the viewport */
  overflow: hidden; /* Prevent any overflow from causing scrollbars */
  display: flex;
  justify-content: center;
}

.hero-image img {
  border-radius: 8px;
  height: 100%; /* Make the image fill the height of its container */
  width: auto; /* Adjust width automatically to maintain aspect ratio */
  object-fit: cover; /* Cover the area, may crop the image if aspect ratios differ */
  object-position: center; /* Center the image within the area */
}

.hero-image::after {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: radial-gradient(circle at center, rgba(255, 255, 255, 0) 25%, #110312 100%);
}
</style>
