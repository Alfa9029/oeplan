<template>
  <div class="valida-container">
    <h2>Validando acesso...</h2>
    <div v-if="status === 'validando'">Por favor, aguarde.</div>
    <div v-if="status === 'sucesso'">Acesso liberado! Redirecionando...</div>
    <div v-if="status === 'erro'">Link inválido ou expirado.</div>
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue'
import { useRoute, useRouter } from 'vue-router'

const status = ref('validando')
const route = useRoute()
const router = useRouter()

onMounted(async () => {
  const token = route.query.token
  if (!token) {
    status.value = 'erro'
    return
  }
  // Aqui você chamaria o backend para validar o token.
  await new Promise((resolve) => setTimeout(resolve, 1200)) // simula requisição
  if (token.length === 43) {
    status.value = 'sucesso'
    setTimeout(() => {
      router.push('/') // leva para painel de tarefas
    }, 1500)
  } else {
    status.value = 'erro'
  }
})
</script>

<style scoped>
.valida-container {
  max-width: 340px;
  margin: 70px auto;
  background: #fff;
  border-radius: 12px;
  box-shadow: 0 2px 12px #0002;
  padding: 32px 28px;
  text-align: center;
}
</style>
