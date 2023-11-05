<script setup>
import { RouterLink } from "vue-router"</script>
<template>
    <header>
        <nav class="container">
            <div class="branding">
                <img src="../assets/bird_logo.png" alt="bird logo of todo app" />
                <h1>To-Do List Web App</h1>
            </div>
            <ul class="nav-routes">
                <RouterLink to="/">Home</RouterLink>
                <RouterLink to="/apiCall">apiCall</RouterLink>
            </ul>
        </nav>
    </header>
</template>
