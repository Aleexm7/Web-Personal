<template>
  <header class="header">
    <nav class="nav container">
      <div class="nav-brand">
        <NuxtLink to="/" class="brand-link">CV Alejandro Muñoz</NuxtLink>
      </div>
      <ul class="nav-menu" :class="{ active: menuOpen }">
        <li><NuxtLink to="/" @click="closeMenu">Inicio</NuxtLink></li>
        <li><NuxtLink to="/proyectos" @click="closeMenu">Proyectos</NuxtLink></li>
        <li><NuxtLink to="/contacto" @click="closeMenu">Contacto</NuxtLink></li>
      </ul>
      <button class="menu-toggle" @click="toggleMenu" aria-label="Toggle menu">
        <span></span>
        <span></span>
        <span></span>
      </button>
    </nav>
  </header>
</template>

<script setup>
import { ref } from 'vue'

const menuOpen = ref(false)

const toggleMenu = () => {
  menuOpen.value = !menuOpen.value
}

const closeMenu = () => {
  menuOpen.value = false
}
</script>

<style scoped>
.header {
  background: var(--bg-color);
  box-shadow: var(--shadow);
  position: sticky;
  top: 0;
  z-index: 100;
}

.nav {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 1rem 20px;
}

.brand-link {
  font-size: 1.5rem;
  font-weight: 700;
  color: var(--primary-color);
  text-decoration: none;
  transition: color 0.3s ease;
}

.brand-link:hover {
  color: var(--primary-dark);
}

.nav-menu {
  display: flex;
  list-style: none;
  gap: 2rem;
  align-items: center;
}

.nav-menu a {
  color: var(--text-color);
  text-decoration: none;
  font-weight: 500;
  transition: color 0.3s ease;
  position: relative;
}

.nav-menu a:hover,
.nav-menu a.router-link-active {
  color: var(--primary-color);
}

.nav-menu a.router-link-active::after {
  content: '';
  position: absolute;
  bottom: -4px;
  left: 0;
  width: 100%;
  height: 2px;
  background: var(--primary-color);
}

.menu-toggle {
  display: none;
  flex-direction: column;
  gap: 4px;
  background: none;
  border: none;
  cursor: pointer;
  padding: 8px;
}

.menu-toggle span {
  width: 24px;
  height: 3px;
  background: var(--text-color);
  border-radius: 2px;
  transition: all 0.3s ease;
}

@media (max-width: 768px) {
  .menu-toggle {
    display: flex;
  }

  .nav-menu {
    position: fixed;
    top: 70px;
    left: 0;
    width: 100%;
    background: var(--bg-color);
    flex-direction: column;
    padding: 2rem;
    box-shadow: var(--shadow);
    transform: translateX(-100%);
    transition: transform 0.3s ease;
    gap: 1.5rem;
  }

  .nav-menu.active {
    transform: translateX(0);
  }

  .nav-menu a.router-link-active::after {
    display: none;
  }
}
</style>

