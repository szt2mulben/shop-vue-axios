<script setup>
import { RouterLink, RouterView } from 'vue-router'
</script>

<template>
  <div class="app-container">
    <nav class="navigation">
      <div class="links">
        <RouterLink class="nav-link" to="/">Bolt</RouterLink>
        <RouterLink class="nav-link" to="/kosar">Kosár</RouterLink>
        <RouterLink class="nav-link" to="/ujtermek">Új termék</RouterLink>
      </div>
    </nav>
    <RouterView />
  </div>
</template>

<style scoped>

.navigation {
  background-color: #078f07; 
  padding: 10px;
}

.links {
  text-align: right; 
}

.nav-link {
  background-color: transparent;
  border: none;
  color: inherit; 
  text-decoration: none; 
  padding: 10px 20px;
  cursor: pointer;
  transition: border-radius 0.3s;
}

.nav-link:hover {
  border-radius: 15px; 
  font-weight: bold;
  font-size: 15px;
  background-color: rgb(67, 121, 67)}
</style>
