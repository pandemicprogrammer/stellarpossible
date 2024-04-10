<template>
  <div class="container">
    <div id="glowing_text" ref="glowingTextRef">{{ dynamicText }}</div>
  </div>
</template>

<script setup>
import { onMounted, ref, watch, toRefs } from 'vue';

// Define props
const props = defineProps({
  text: String
});

const { text } = toRefs(props);
const dynamicText = ref('');

// Copy the initial text value to dynamicText
dynamicText.value = text.value;

const glowingTextRef = ref(null);

onMounted(() => {
  const startGlowing = () => {
    let index = 0;
    const intervalId = setInterval(() => {
      if (!glowingTextRef.value) return;
      
      const letters = dynamicText.value.split('');
      if (letters[index] === ' ') {
        index++;
      }
      
      letters[index] = `<span style="color: var(--glowColor); text-shadow: var(--shadowColor);">${letters[index]}</span>`;
      const coloredText = letters.join('');
      glowingTextRef.value.innerHTML = coloredText;
      index = (index + 1) % letters.length;
    }, 500);
    
    return () => clearInterval(intervalId);
  };

  startGlowing();
});
</script>

<style>

:root {
  --screenCoeff: calc(1vw + 1vh);
  --bgColor: rgb(20, 20, 20);
  --fontColor: rgb(255, 255, 255);
  --shadowColor: 0 0 0.3em rgb(0 229 215);
  --glowColor: rgb(160 255 234);
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
}
.container:first-of-type {
      top: 40%;
}
.container:last-of-type {
      top: 58%;
}
#glowing_text {
  text-wrap: nowrap;
  text-overflow: clip;
}
</style>
