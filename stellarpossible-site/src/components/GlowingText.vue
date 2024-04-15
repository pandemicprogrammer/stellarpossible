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

const startGlowing = () => {
  let index = 0;
  const totalAnimationTime = 1000; // Adjust as needed
  const letters = dynamicText.value.split('');
  const intervalDuration = totalAnimationTime / letters.filter(letter => letter.trim() !== '').length;

  intervalId = setInterval(() => {
    if (!glowingTextRef.value) return;

    if (index >= letters.length) {
      clearInterval(intervalId);
      glowingTextRef.value.innerHTML = dynamicText.value; // Reset text
      return;
    }

    letters[index] = letters[index].trim() === '' ? letters[index] : `<span class="glow">${letters[index]}</span>`;
    glowingTextRef.value.innerHTML = letters.join('');

    index++;
  }, intervalDuration);
};

const stopGlowing = () => {
  clearInterval(intervalId);
  if (glowingTextRef.value) glowingTextRef.value.innerHTML = dynamicText.value; // Clear styles
};

const resetAnimation = () => {
  stopGlowing();
  startGlowing();
};

onMounted(() => {
  startGlowing();
});

onUnmounted(() => {
  stopGlowing();
});
</script>


<style>

:root {
  --screenCoeff: calc(1vw + 1vh);
  --bgColor: rgb(20, 20, 20);
  --fontColor: rgb(255, 255, 255, .45);
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
  font-weight: bold;
}

.glow {
  display: inline-block; /* Required for transforming individual letters */
  transition: transform 0.5s ease, opacity 0.5s ease; /* Smooth transition for scaling and fading */
  transform: scale(1.05); /* Slightly scale up the letters */
  color: var(--glowColor);
  text-shadow: var(--shadowColor);
  opacity: 0; /* Start with the letter being invisible */
  animation: glowEffect 1s forwards; /* Animation to control the visibility and scaling */
}

@keyframes glowEffect {
  0% {
    transform: scale(1);
    opacity: 0;
  }
  50% {
    opacity: 1;
  }
  100% {
    transform: scale(1.05);
    opacity: 0;
  }
}
</style>
