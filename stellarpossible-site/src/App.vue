<script setup>
import { RouterLink, RouterView } from 'vue-router';
</script>

<template>
  <header>
    <div class="wrapper">
      <!-- Wrap "StellarPossible" in a RouterLink to route back to home ("/") -->
      <div class="logo">
        <RouterLink to="/">StellarPossible</RouterLink>
      </div>
      <nav>
        <RouterLink to="/">Home</RouterLink>
        <RouterLink to="/Products">
          Products
        </RouterLink>
      </nav>
    </div>
  </header>

  <RouterView />
</template>

<style scoped>
.wrapper {
    display: flex;
    justify-content: space-between;
}
/* Additional styling for the RouterLink to make it look consistent with your design */
.logo a {
    text-decoration: none;
    color: inherit; /* This ensures the link color matches your logo color */
}
</style>
