<template>
  <footer class="footer">
    <div class="container">
      <p>&copy; {{ currentYear }} - Todos los derechos reservados</p>
    </div>
  </footer>
</template>

<script setup>
const currentYear = new Date().getFullYear()
</script>

<style scoped>
.footer {
  background: var(--bg-light);
  padding: 2rem 0;
  text-align: center;
  color: var(--text-light);
  margin-top: auto;
}
</style>

