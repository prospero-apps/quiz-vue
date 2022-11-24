<script setup>
  import { RouterView } from 'vue-router'
</script>

<template>
  <div class="container">
    <RouterView />
  </div>
</template>

<style scoped>
  .container {
    max-width: 1200px;
    margin: auto;
    height: 100vh;
    background-color: rgb(235, 228, 228);
  }
</style>