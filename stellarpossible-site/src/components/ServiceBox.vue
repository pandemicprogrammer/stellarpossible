<template>
  <div class="service-box">
    <img :src="icon" alt="Service Icon">
    <h3>{{ title }}</h3>
    <p>{{ description }}</p>
  </div>
</template>

<script setup>
// Define props for the service box
defineProps(['icon', 'title', 'description']);
</script>

<style scoped>
/* Add service box styles here */
.service-box {
  /* Styling for the service box */
}
</style>
