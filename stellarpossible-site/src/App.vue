<script setup>
import { RouterLink, RouterView } from 'vue-router';
import logo from './assets/images/stellarpossible-logo.png'
</script>

<template>
  <header>
    <div class="wrapper">
      <!-- Wrap "StellarPossible" in a RouterLink to route back to home ("/") -->
      <div class="logo">
        <RouterLink to="/">
                <img class="logo" :src="logo" alt="Logo" />
        </RouterLink>
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
.logo {
  width: 10rem;
}
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
