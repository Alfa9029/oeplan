<template>
  <div class="login-admin">
    <h2>Login Administrativo</h2>
    <form @submit.prevent="login">
      <input v-model="email" type="email" placeholder="E-mail" required />
      <input v-model="senha" type="password" placeholder="Senha" required />
      <button type="submit" :disabled="loading">
        {{ loading ? 'Entrando...' : 'Entrar' }}
      </button>
    </form>
    <div v-if="erro" class="erro">{{ erro }}</div>
  </div>
</template>

<script setup>
import { ref } from 'vue'

const email = ref('')
const senha = ref('')
const erro = ref('')
const loading = ref(false)

async function login() {
  loading.value = true
  erro.value = ''
  // Simula validação de login admin
  await new Promise((resolve) => setTimeout(resolve, 1200))
  loading.value = false
  if (email.value === 'admin@email.com' && senha.value === '123456') {
    // Salvar token/cookie e redirecionar para dashboard admin
    window.location.href = '/admin-dashboard' // coloque a rota real depois
  } else {
    erro.value = 'E-mail ou senha inválidos'
  }
}
</script>

<style scoped>
.login-admin {
  max-width: 350px;
  margin: 60px auto;
  padding: 36px 28px;
  background: #fff;
  border-radius: 12px;
  box-shadow: 0 2px 16px #0002;
  text-align: center;
}
input {
  width: 100%;
  padding: 12px;
  border-radius: 8px;
  margin-bottom: 14px;
  border: 1px solid #ddd;
  font-size: 16px;
}
button {
  padding: 12px 28px;
  border: none;
  background: #f66a0a;
  color: #fff;
  font-weight: bold;
  border-radius: 8px;
  cursor: pointer;
  transition: background 0.2s;
}
button[disabled] {
  background: #bbb;
}
.erro {
  margin-top: 16px;
  color: #d00;
}
</style>
