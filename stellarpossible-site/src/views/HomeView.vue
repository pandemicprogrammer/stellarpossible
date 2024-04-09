<template>
  <main>
    <div class="wrapper">
      <div class="hero-image">
        <img :src="HeroImage" alt="Galaxy Hero" />
      </div>
      <div class="tagline-wrapper">    
        <div class="tagline-text">
          <span>To Inspire.</span>
          <span>To Be Inspired.</span>
        </div>
      </div>
    </div>
  </main>
</template>

<script setup>
import HeroImage from '../assets/images/galaxy-hero.png';
</script>

<style scoped>
.wrapper {
  position: relative;
}
.tagline-wrapper {
  position: absolute;
  height: 100vh;
  width: 100%;
  top: 0;
}
.tagline-text {
  color: white;
  display: flex;
  justify-content: center;
  align-items: center;
  height: 87%;
}
.hero-image {
  position: relative;
  height: 90vh; /* Set the height of the hero image to fill the viewport */
  overflow: hidden;
  display: flex;
  justify-content: center; /* This centers the image horizontally */
}

.hero-image img {
  border-radius: 8px;
  height: 100%;
  width: auto; /* Width is auto to maintain aspect ratio */
  object-fit: cover;
  object-position: center;
}

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
  margin-left: -2.5rem;
}

.hero-image::after {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: radial-gradient(circle at center, rgba(255, 255, 255, 0) 75%, #110312 100%);
}
</style>
