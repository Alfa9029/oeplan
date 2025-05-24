<template>
  <button class="theme-toggle" @click="toggleTheme" :aria-label="temaAtual==='dark'?'Tema claro':'Tema escuro'">
    <span v-if="temaAtual === 'dark'">🌞</span>
    <span v-else>🌙</span>
  </button>
</template>

<script setup>
import { ref, onMounted } from 'vue'
const temaAtual = ref('light')

onMounted(() => {
  const salvo = localStorage.getItem('tema-oeplan')
  if (salvo) {
    temaAtual.value = salvo
    document.documentElement.setAttribute('data-theme', salvo)
  } else if (window.matchMedia && window.matchMedia('(prefers-color-scheme: dark)').matches) {
    temaAtual.value = 'dark'
    document.documentElement.setAttribute('data-theme', 'dark')
  }
})

function toggleTheme() {
  temaAtual.value = temaAtual.value === 'dark' ? 'light' : 'dark'
  document.documentElement.setAttribute('data-theme', temaAtual.value)
  localStorage.setItem('tema-oeplan', temaAtual.value)
}
</script>

<style scoped>
.theme-toggle {
  background: none;
  border: none;
  cursor: pointer;
  font-size: 1.7rem;
  margin-left: 12px;
  transition: filter 0.15s;
  filter: brightness(0.85);
}
.theme-toggle:hover {
  filter: brightness(1.1);
}
</style>
