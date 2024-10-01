<script setup>
import { RouterLink, RouterView } from "vue-router";
</script>

<template>
  <div class="container-fluid p-4">
    <header class="mb-4 text-center position-relative">
      <h1 class="display-3">
        <span class="led-title">Szakkörök</span>
      </h1>

      <div class="separator"></div> 

      <ul class="nav justify-content-center mb-4">
        <li>
          <RouterLink
            :to="{ path: '/' }"
            :class="{ active: $route.path === '/' }"
          >
            <i class="fa fa-plus"></i>
          </RouterLink>
        </li>
      </ul>
    </header>

    <div class="content-area border rounded p-4">
      <RouterView />
    </div>
  </div>
</template>

<style>
body {
  background: black; /* Set background to black */
  height: 100%;
  user-select: none;
  color: var(--color); /* Set text color */
}

.separator {
  animation-delay: 0.6s; /* Késleltetés az első LED elválasztónál */
}


@keyframes glow {
  0% {
    opacity: 0.5; /* Kezdeti fényesség */
  }
  100% {
    opacity: 1; /* Maximális fényesség */
  }
}

header {
  position: relative;
}

.display-3 {
  font-weight: 400;
  position: relative;
}

/* LED-style title text */
.led-title {
  display: inline-block;
  position: relative;
  color: var(--color); /* Title text color */
  text-shadow: 
    0 0 5px rgba(76, 0, 255, 1), /* Glow effect */
    0 0 10px rgba(0, 187, 255, 0.7); /* Additional glow */
}

/* LED-style separator line */
.separator {
  height: 5px; /* Elválasztó vonal magassága */
  width: 90%; /* Szélesség */
  margin: 20px 0; /* Tér az elválasztó körül */
  background: linear-gradient(90deg, #4c00ff, #00bfff, #4c00ff); /* LED-szerű hatás */
  border-radius: 5px; /* Lekerekített sarkok */
  box-shadow: 0 0 10px rgba(76, 0, 255, 0.5), 0 0 20px rgba(0, 187, 255, 0.5); /* Fényhatás */
  animation: glow 1.5s infinite alternate; /* Pulzáló animáció */
}

/* Other styles remain unchanged */
.content-area {
  border-radius: 5px;
  box-shadow: 0 0 20px rgba(0, 0, 0, 0.15);
}

.nav li a {
  font-size: 16px;
  font-weight: 600;
  display: block;
  color: var(--color); /* Set link color to the color variable */
  padding: 5px 15px;
  text-decoration: none;
  transition: 0.5s;
}

.nav li a:hover {
  color: var(--color);
}

.nav li a.active {
  color: var(--color);
  font-weight: 700;
}

.form-check-input:checked {
  background-color: var(--color);
  border-color: var(--color);
}
</style>
