<script setup>
import { RouterLink, RouterView } from 'vue-router';
import logo from './assets/images/stellarpossible-logo.png';
import hamburgerIcon from './assets/images/hamburger.png'; // Make sure the path is correct
</script>

<template>
  <header>
    <div class="wrapper">
      <RouterLink to="/" class="logo">
        <img :src="logo" alt="Logo" />
      </RouterLink>
      <nav>
        <RouterLink to="/">Home</RouterLink>
        <RouterLink to="/Products">Products</RouterLink>
        <RouterLink to="/Blog">Blog</RouterLink>
      </nav>
      <div class="menu-icon">
        <img :src="hamburgerIcon" alt="Menu" />
      </div>
    </div>
  </header>
  <RouterView />
</template>

<style scoped>
.logo img {
  width: 12rem;
  margin-left: -1rem;
}
.wrapper {
  display: flex;
  justify-content: center;
  align-items: center;
}
nav {
  display: flex;
  align-items: center;
}
nav a {
  margin-left: 5px;
}
.menu-icon {
  display: none; /* Initially hidden */
}
/* Responsive Styles */
@media (max-width: 400px) {
  .wrapper {
    justify-content: space-around;
  }
  nav {
    display: none; /* Hide the nav links on small screens */
  }
  .menu-icon {
    display: block; /* Show the menu icon on small screens */
    cursor: pointer;
  }
  .menu-icon img {
    width: 1.25rem;
  }
}
</style>
