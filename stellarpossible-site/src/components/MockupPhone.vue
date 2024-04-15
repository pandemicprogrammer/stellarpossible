<template>
  <section class="mockup-phone">
    <img :src="TeletherapyImage" alt="Teletherapy Image" />
  </section>
</template>

<script setup>
    import TeletherapyImage from '../assets/images/teletherapy-tool.png';
</script>

<style scoped>
/* Add hero section styles here */
.mockup-phone img{
    width: 10rem;
}
</style>
