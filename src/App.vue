<script setup>
import { RouterLink, RouterView } from 'vue-router'

</script>

<template>
  <header class="bg-gray-700 p-5">
    <div class="container flex items-center justify-between">

      <nav>
        <RouterLink to="/">Home</RouterLink>
        <RouterLink to="/carousel">Carousel</RouterLink>
        <RouterLink to="/piechart">PieChart</RouterLink>

      </nav>
    </div>
  </header>

  <RouterView />
</template>

<style scoped>
a{
  color: #fff;
  text-decoration: none;
  padding: 10px;
  margin: 10px;
  border-radius: 5px;
  background: #4a5568;
  transition: all 0.3s ease-in-out;
}
</style>
