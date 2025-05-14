<template>
  <div class="login-container">
    <!-- Painel esquerdo: logo + descrição -->
    <div class="left-panel">
      <Logo class="logo" />
      <h1 class="title">
        OEPlan<br />
        Sistema para Gerenciamento<br />
        de Atividades Docentes
      </h1>
    </div>

    <!-- Painel direito: card de login -->
    <div class="right-panel">
      <div class="card">
        <h2 class="card__title">Login</h2>
        <form @submit.prevent="onSubmit" class="card__form">
          <label for="email">Email</label>
          <input
            id="email"
            type="email"
            v-model="form.email"
            placeholder="name@example.com"
            required
          />

          <label for="password">Senha</label>
          <div class="password-field">
            <input
              id="password"
              :type="showPassword ? 'text' : 'password'"
              v-model="form.password"
              placeholder="••••••••"
              required
            />
            <button type="button" @click="togglePassword" class="toggle">
              {{ showPassword ? '🙈' : '👁️' }}
            </button>
          </div>

          <div class="forgot">
            <NuxtLink to="/reset-password">Esqueceu a senha?</NuxtLink>
          </div>

          <button type="submit" class="btn-primary">Entrar</button>

          <p class="help">
            Precisa de ajuda?
            <NuxtLink to="/contact">Entre em contato</NuxtLink>
          </p>
        </form>
      </div>
    </div>
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue'
import Logo from '~/components/Logo.vue'

const form = ref({ email: '', password: '' })
const showPassword = ref(false)

function togglePassword() {
  showPassword.value = !showPassword.value
}

function onSubmit() {
  // Aqui você chamaria sua API de login (por exemplo, via fetch ou $fetch do Nuxt).
  alert(`Login com ${form.value.email}`)
}
</script>

<style scoped>
.login-container {
  display: flex;
  min-height: 100vh;
}

/* Esquerda: fundo escuro */
.left-panel {
  flex: 1;
  background: #080b19;
  color: #fff;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  text-align: center;
  padding: 2rem;
}
.left-panel .logo {
  width: 96px;
  margin-bottom: 1.5rem;
}
.left-panel .title {
  line-height: 1.4;
  font-size: 1.25rem;
  font-weight: 500;
}

/* Direita: card branco */
.right-panel {
  flex: 1;
  background: #080b19;
  display: flex;
  align-items: center;
  justify-content: center;
  padding: 2rem;
}
.card {
  background: #ffffff;
  border-radius: 8px;
  padding: 2rem;
  width: 100%;
  max-width: 360px;
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.1);
}
.card__title {
  text-align: center;
  margin-bottom: 1.5rem;
  color: #0f1f27;
}
.card__form label {
  display: block;
  margin-top: 1rem;
  font-size: 0.9rem;
  color: #0f1f27;
}
.card__form input {
  width: 100%;
  padding: 0.5rem;
  margin-top: 0.25rem;
  border: 1px solid #e2e8f0;
  border-radius: 4px;
  font-size: 1rem;
}
.password-field {
  position: relative;
}
.password-field .toggle {
  position: absolute;
  right: 0.5rem;
  top: 50%;
  transform: translateY(-50%);
  background: none;
  border: none;
  cursor: pointer;
}
.forgot {
  text-align: right;
  margin-top: 0.5rem;
}
.forgot a {
  font-size: 0.85rem;
  color: #2fa7b8;
}
.btn-primary {
  width: 100%;
  margin-top: 1.5rem;
  padding: 0.75rem;
  background: #0f1f27;
  color: #fff;
  border: none;
  border-radius: 4px;
  cursor: pointer;
}
.help {
  text-align: center;
  margin-top: 1rem;
  font-size: 0.85rem;
}
.help a {
  color: #2fa7b8;
}
</style>
