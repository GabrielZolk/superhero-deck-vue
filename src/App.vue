<script setup>
import Navbar from './components/Navbar.vue';
</script>

<template>
    <div>
      <Navbar />
    </div>
  <RouterView />
</template>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
</style>
