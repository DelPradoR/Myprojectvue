<script setup>
import { RouterLink, RouterView } from 'vue-router'
import HelloWorld from './components/HelloWorld.vue'
</script>

<template>
  <header>
    <img alt="Vue logo" class="logo" src="@/assets/logo.svg" width="125" height="125" />

    <div class="wrapper">
      <HelloWorld msg="You did it!" />

      <nav>
        <RouterLink to="/" class="nav-link">Home</RouterLink>
        <RouterLink to="/about" class="nav-link">About</RouterLink>
        <RouterLink to="/peliculas" class="nav-link">Peliculas</RouterLink>
      </nav>
    </div>
  </header>

  <RouterView />
</template>

<style scoped>
body {
    background-color: white; /* Fondo blanco para la página */
    margin: 0; /* Elimina el margen predeterminado */
    font-family: Arial, sans-serif; /* Cambia la fuente según tus preferencias */
}

header {
  line-height: 1.5;
  max-height: 100vh;
}

.logo {
  display: block;
  margin: 0 auto 2rem;
}

nav {
  width: 100%;
  font-size: 12px;
  text-align: center;
  margin-top: 2rem;
}

nav a.router-link-exact-active {
  color: black; /* Color negro para el enlace activo */
}

nav a.router-link-exact-active:hover {
  background-color: transparent;
}

nav a {
  display: inline-block;
  padding: 0 1rem;
  border-left: 1px solid var(--color-border);
}

nav a:first-of-type {
  border: 0;
}

.nav-link {
  color: black; /* Color negro para los enlaces */
  text-decoration: none; /* Elimina el subrayado */
}

.nav-link:hover {
  color: rgb(4, 0, 255); /* Color gris al pasar el mouse */
}

@media (min-width: 1024px) {
  header {
    display: flex;
    place-items: center;
    padding-right: calc(var(--section-gap) / 2);
  }

  .logo {
    margin: 0 2rem 0 0;
  }

  header .wrapper {
    display: flex;
    place-items: flex-start;
    flex-wrap: wrap;
  }

  nav {
    text-align: left;
    margin-left: -1rem;
    font-size: 1rem;

    padding: 1rem 0;
    margin-top: 1rem;
  }
}
</style>