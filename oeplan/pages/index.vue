<!-- pages/index.vue -->
<template>
  <div class="redirecting">
    <p>Redirecionando para o Login…</p>
  </div>
</template>

<script setup lang="ts">
import { onMounted } from 'vue'
import { useRouter } from 'vue-router'

const router = useRouter()

onMounted(() => {
  router.replace('/login')
})
</script>

<style scoped>
.redirecting {
  display: flex;
  align-items: center;
  justify-content: center;
  height: 100vh;
  color: #ffffffcc;
  background: #080b19;
  font-size: 1.1rem;
}
</style>
