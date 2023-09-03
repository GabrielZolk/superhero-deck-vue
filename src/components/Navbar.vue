<template>
    <header class="header">
        <h1>Superhero Deck</h1>
        <nav class="nav">
            <RouterLink to="/">Home</RouterLink>
        </nav>
    </header>
</template>

<script setup>
import { RouterLink, RouterView } from 'vue-router'
</script>

<style scoped>
.header {
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 1rem;
    background-color: #4c0edf;
    color: white;
}

.nav {
    display: flex;
    gap: 1rem;
    list-style: none;
    padding: 1rem;
    background-color: #4c0edf;
    border-radius: 5px;
    font-weight: bold;
    font-size: 1.2rem;
    cursor: pointer;
    transition: all 0.3s;
    
}

.nav a {
    text-decoration: none;
    color: white;
}
</style>