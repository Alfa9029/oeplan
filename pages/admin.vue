<template>
  <div class="login-split-bg">
    <!-- LADO ESQUERDO -->
    <div class="login-left">
      <div class="login-left-content">
        <img src="assets/logo.png" alt="Logo OEPlan" class="login-logo" />
        <div class="login-left-title">
          OEPlan - Sistema para Gerenciamento<br>
          de Atividades Docentes
        </div>
      </div>
    </div>
    <!-- LADO DIREITO -->
    <div class="login-right">
      <div class="login-card">
        <h2 class="login-card-title">Login</h2>
        <form @submit.prevent="login" autocomplete="off">
          <div class="login-label">Email</div>
          <input
            type="email"
            v-model="email"
            placeholder="name@example.com"
            class="login-input"
            required
            autocomplete="username"
          />

          <div class="login-pw-row">
            <span class="login-label">Senha</span>
            <span class="pw-link" @click.prevent="recuperarSenha">Esqueceu a senha?</span>
          </div>
          <div class="login-pw-input">
            <input
              :type="showPw ? 'text' : 'password'"
              v-model="senha"
              placeholder="••••••••"
              class="login-input-pw"
              required
              autocomplete="current-password"
            />
            <span class="pw-eye" @click="showPw = !showPw" :title="showPw?'Ocultar':'Mostrar senha'">
              <!-- Ícone visibilidade -->
              <svg v-if="showPw" xmlns="http://www.w3.org/2000/svg" width="21" height="21" fill="none" viewBox="0 0 24 24"><path stroke="#444" stroke-width="1.7" d="M12 4C6.5 4 2 8.5 2 12c0 3.5 4.5 8 10 8s10-4.5 10-8c0-3.5-4.5-8-10-8zm0 0c1.7 0 3.3.7 4.5 1.8M2 12c1.7-3.7 5.8-7 10-7s8.3 3.3 10 7M9.5 14.5c-.5-.8-.5-1.7 0-2.5.5-.8 1.3-1.3 2.1-1.3.8 0 1.6.5 2.1 1.3.5.8.5 1.7 0 2.5-.5.8-1.3 1.3-2.1 1.3-.8 0-1.6-.5-2.1-1.3z"/></svg>
              <svg v-else xmlns="http://www.w3.org/2000/svg" width="21" height="21" fill="none" viewBox="0 0 24 24"><path stroke="#444" stroke-width="1.7" d="M4.2 4.2L19.8 19.8M7.1 7.1C5.3 8.7 4 10.3 4 12c0 3.5 4.5 8 10 8 2.3 0 4.3-.8 6-2.1M12 4c3.5 0 6.7 1.7 8.7 4.2"/><circle cx="12" cy="12" r="3" stroke="#444" stroke-width="1.7"/></svg>
            </span>
          </div>

          <button type="submit" class="login-btn">Entrar</button>
        </form>
        <div class="login-footer">
          <span>Precisa de ajuda?</span>
          <a href="#" @click.prevent="contato">Entre em contato</a>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue'
const email = ref('')
const senha = ref('')
const showPw = ref(false)

function login() {
  if (!email.value || !senha.value) return alert('Preencha todos os campos')
  alert(`Login:\n${email.value} / ${senha.value}`)
}
function recuperarSenha() {
  alert('Funcionalidade "esqueceu a senha" em construção!')
}
function contato() {
  alert('Abrir suporte (implementar)')
}
</script>

<style scoped>
@import url('https://fonts.googleapis.com/css2?family=Inter:wght@600;700;900&display=swap');

html, body {
  height: 100%;
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  background: #101116 !important;
}

.login-split-bg {
  display: flex;
  min-height: 100vh;
  width: 100vw;
  background: #101116;
  font-family: 'Inter', 'Segoe UI', Arial, sans-serif;
  overflow: hidden;
}

.login-left {
  flex: 1 1 0;
  display: flex;
  align-items: center;
  justify-content: center;
  background: linear-gradient(135deg, #09090c 74%, #131417 100%);
  min-width: 350px;
  height: 100vh;
}

.login-left-content {
  display: flex;
  flex-direction: column;
  align-items: center;
}
.login-logo {
  width: 74px;
  height: 74px;
  margin-bottom: 38px;
  border-radius: 50%;
  background: #23262e;
  box-shadow: 0 2px 24px #0006;
  object-fit: contain;
}
.login-left-title {
  color: #fff;
  font-weight: 900;
  font-size: 1.33rem;
  line-height: 1.34;
  text-align: center;
  letter-spacing: -0.005em;
  margin-top: 6px;
  text-shadow: 0 1px 10px #0006;
}

.login-right {
  flex: 1 1 0;
  display: flex;
  justify-content: center;
  align-items: center;
  background: #181b22;
  min-height: 100vh;
  min-width: 0;
  height: 100vh;
}

.login-card {
  width: 265px;
  padding: 26px 18px 15px 18px;
  background: #fff;
  border-radius: 13px;
  box-shadow: 0 8px 42px #0002;
  display: flex;
  flex-direction: column;
  align-items: stretch;
  margin: 0 auto;
}

.login-card-title {
  text-align: center;
  margin-bottom: 16px;
  font-weight: 700;
  font-size: 1.19rem;
  color: #131b1d;
  letter-spacing: -0.01em;
}

form {
  display: flex;
  flex-direction: column;
  gap: 6px;
}
.login-label {
  font-size: 0.99rem;
  font-weight: 600;
  margin-bottom: 3px;
  color: #252d34;
  letter-spacing: -0.01em;
}
.login-input, .login-input-pw {
  width: 100%;
  padding: 9px 11px;
  font-size: 1rem;
  border-radius: 7px;
  border: 1.3px solid #dbe1ea;
  background: #f7fafd;
  margin-bottom: 1px;
  font-family: inherit;
  transition: border 0.18s;
}
.login-input:focus, .login-input-pw:focus {
  border: 1.6px solid #22687d;
  outline: none;
}
.login-pw-row {
  display: flex;
  justify-content: space-between;
  align-items: center;
  font-size: 1rem;
  margin-top: 10px;
  margin-bottom: 2px;
}
.pw-link {
  color: #195f76;
  cursor: pointer;
  font-size: 0.97rem;
  font-weight: 500;
  transition: text-decoration 0.13s;
}
.pw-link:hover { text-decoration: underline; }
.login-pw-input {
  display: flex;
  align-items: center;
  background: #f7fafd;
  border: 1.3px solid #dbe1ea;
  border-radius: 7px;
  padding-right: 6px;
  margin-bottom: 10px;
}
.login-input-pw {
  border: none;
  background: transparent;
  margin: 0;
  flex: 1 1 0;
  font-size: 1rem;
  padding: 9px 11px;
  outline: none;
  font-family: inherit;
}
.pw-eye {
  cursor: pointer;
  margin-left: 4px;
  display: flex;
  align-items: center;
  opacity: 0.7;
}
.pw-eye:hover { opacity: 1; }
.login-btn {
  background: #193b3e;
  color: #fff;
  border: none;
  border-radius: 7px;
  font-weight: 700;
  font-size: 1.03rem;
  padding: 11px 0;
  margin-top: 7px;
  margin-bottom: 3px;
  cursor: pointer;
  letter-spacing: 0.01em;
  transition: background 0.18s;
  font-family: inherit;
}
.login-btn:hover {
  background: #22687d;
}
.login-footer {
  text-align: left;
  font-size: 0.94rem;
  margin-top: 10px;
  color: #49545c;
  font-family: inherit;
}
.login-footer a {
  color: #195f76;
  text-decoration: none;
  margin-left: 5px;
  font-size: 0.99rem;
  font-weight: 700;
}
.login-footer a:hover { text-decoration: underline; }

@media (max-width: 900px) {
  .login-split-bg { flex-direction: column; }
  .login-left, .login-right { flex: none; min-height: 220px; justify-content: flex-start; }
  .login-left { padding-top: 40px; padding-bottom: 20px; }
  .login-right { padding-top: 40px; padding-bottom: 40px; }
  .login-card { width: 98vw; max-width: 280px; }
}
</style>
