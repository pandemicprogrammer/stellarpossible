<template>
  <div class="container">
    <div id="glowing_text" ref="glowingTextRef" @mouseover="resetAnimation" @click="resetAnimation">{{ dynamicText }}</div>
  </div>
</template>
<script setup>
import { onMounted, ref, toRefs, onUnmounted } from 'vue';

const props = defineProps({
  text: String
});

const { text } = toRefs(props);
const dynamicText = ref('');
dynamicText.value = text.value;

const glowingTextRef = ref(null);

let intervalId = null;

// Method to start glowing effect
const startGlowing = () => {
  let index = 0;
  const totalAnimationTime = 1000; // Total animation time in milliseconds
  const intervalDuration = totalAnimationTime / dynamicText.value.replace(/\s+/g, '').length;

  intervalId = setInterval(() => {
    if (!glowingTextRef.value) return;
    
    const letters = dynamicText.value.split('');
    if (index >= letters.length) {
      clearInterval(intervalId);
      glowingTextRef.value.innerHTML = dynamicText.value; // Reset text to remove styles after complete
      return;
    }
    if (letters[index] === ' ') {
      index++; // Increment index if current character is a space
    }
    
    letters[index] = `<span style="color: var(--glowColor); text-shadow: var(--shadowColor);">${letters[index]}</span>`;
    glowingTextRef.value.innerHTML = letters.join('');
    
    index++;
  }, intervalDuration);
};

// Method to stop glowing effect and clear styles
const stopGlowing = () => {
  clearInterval(intervalId);
  if (glowingTextRef.value) glowingTextRef.value.innerHTML = dynamicText.value; // Remove all styling
};

// Reset and start animation on hover or click
const resetAnimation = () => {
  stopGlowing(); // Clear any existing animation
  startGlowing(); // Start the animation again
};

onMounted(() => {
  startGlowing(); // Start the animation when the component is mounted
});

onUnmounted(() => {
  stopGlowing(); // Clean up on component unmount
});
</script>


<style>

:root {
  --screenCoeff: calc(1vw + 1vh);
  --bgColor: rgb(20, 20, 20);
  --fontColor: rgb(255, 255, 255, .75);
  --shadowColor: 0 0 0.3em rgb(255, 255, 255);
  --glowColor: rgb(255, 255, 255);
}

* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

body {
  background-color: var(--bgColor);
}

.container {
  position: absolute;
  left: 50%;
  transform: translate(-50%, -50%);
  color: var(--fontColor);
  font-family: "M PLUS 1 Code", monospace;
  font-size: 1.2rem;

}
.container:first-of-type {
      top: 18%;
}
.container:last-of-type {
      top: 85%;
}
#glowing_text {
  text-wrap: nowrap;
  text-overflow: clip;
  cursor: pointer; /* Indicates the text is clickable */
  display: inline-block; /* Ensures the hover area is only around the text */
}
</style>
