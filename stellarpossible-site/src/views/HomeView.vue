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
import gsap from 'gsap';
import { onMounted } from 'vue';

onMounted(() => {
  // Define the start and end elements
  const startElement = document.querySelector('.tagline-text span:first-child');
  const endElement = document.querySelector('.tagline-text span:last-child');

  // Get positions of the start and end elements
  const startPosition = startElement.getBoundingClientRect();
  const endPosition = endElement.getBoundingClientRect();

  // Create a dummy element for the animation (a simple line)
  const line = document.createElement('div');
  line.style.position = 'absolute';
  line.style.height = '2px';
  line.style.width = '0';
  line.style.backgroundColor = 'white';
  line.style.top = `${startPosition.top + startPosition.height / 2}px`;
  line.style.left = `${startPosition.left + startPosition.width / 2}px`;
  document.body.appendChild(line);

  // Animate the line from start to end
  gsap.to(line, {
    width: Math.sqrt(Math.pow(endPosition.left - startPosition.left, 2) + Math.pow(endPosition.top - startPosition.top, 2)) + 'px',
    x: endPosition.left - startPosition.left,
    y: endPosition.top - startPosition.top,
    duration: 2,
    ease: "power2.out"
  });
});


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
  flex-flow: column;
  justify-content: space-evenly;
  align-items: center;
  height: 88%;
}
.tagline-text span {
  font-weight: 600;
  padding: 3px;
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
