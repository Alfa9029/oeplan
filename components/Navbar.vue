<template>
  <nav>
    <NuxtLink to="/">Home</NuxtLink>
    <NuxtLink to="/groups">Grupos</NuxtLink>
    <NuxtLink to="/archived">Arquivadas</NuxtLink>
    <NuxtLink to="/help">Ajuda</NuxtLink>
    <NuxtLink to="/admin">Admin</NuxtLink>
    <ThemeToggle />
  </nav>
</template>
<script setup>
import ThemeToggle from '~/components/ThemeToggle.vue'
</script>
<style scoped>
nav {
  display: flex;
  gap: 20px;
  padding: 16px;
  background: var(--card-bg);
  border-bottom: 1px solid #eee;
}
a {
  text-decoration: none;
  color: var(--text-main);
  font-weight: 500;
}
a.router-link-active {
  color: var(--primary);
}
</style>
