<template>
  <div class="magic-link-container">
    <h2>Acesso por E-mail</h2>
    <form @submit.prevent="enviarMagicLink">
      <input
        v-model="email"
        type="email"
        placeholder="Digite seu e-mail institucional"
        required
      />
      <button type="submit" :disabled="loading">
        {{ loading ? 'Enviando...' : 'Receber Link de Acesso' }}
      </button>
    </form>
    <div v-if="msg" class="msg">{{ msg }}</div>
  </div>
</template>

<script setup>
import { ref } from 'vue'

const email = ref('')
const msg = ref('')
const loading = ref(false)

async function enviarMagicLink() {
  loading.value = true
  msg.value = ''
  // Simula chamada para backend
  await new Promise((resolve) => setTimeout(resolve, 1500))
  loading.value = false
  msg.value = 'Verifique seu e-mail! Enviamos um link de acesso.'
  email.value = ''
}
</script>

<style scoped>
.magic-link-container {
  max-width: 380px;
  margin: 60px auto;
  background: #fff;
  border-radius: 14px;
  padding: 40px 32px;
  box-shadow: 0 4px 24px #0001;
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
.msg {
  margin-top: 18px;
  color: #2e8b57;
}
</style>
