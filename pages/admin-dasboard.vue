<template>
  <div class="admin-container">
    <header class="admin-header">
      <h1>Painel Administrativo</h1>
      <button @click="logout" class="logout-btn">Sair</button>
    </header>

    <nav class="admin-menu">
      <button :class="{active: menu === 'usuarios'}" @click="menu = 'usuarios'">Gestão de Usuários</button>
      <button :class="{active: menu === 'relatorios'}" @click="menu = 'relatorios'">Relatórios</button>
      <button :class="{active: menu === 'monitoramento'}" @click="menu = 'monitoramento'">Monitoramento</button>
      <button :class="{active: menu === 'backup'}" @click="menu = 'backup'">Backup/Configurações</button>
    </nav>

    <section class="admin-section">
      <GestaoUsuarios v-if="menu === 'usuarios'" />
      <Relatorios v-if="menu === 'relatorios'" />
      <Monitoramento v-if="menu === 'monitoramento'" />
      <BackupConfig v-if="menu === 'backup'" />
    </section>
  </div>
</template>


<script setup>

import { useRouter } from 'vue-router'
import { ref } from 'vue'

// Simulação de login admin. Depois use token/cookie ou middleware!
const menu = ref('usuarios')
const isAdmin = true // simule o admin autenticado
const router = useRouter()
if (!isAdmin) {
  router.push('/admin') // redireciona se não for admin
}



function logout() {
  // Aqui pode limpar token/cookie e redirecionar
  window.location.href = '/admin'
}

// Componentes das seções (crie em /components/admin/)
import GestaoUsuarios from '~/components/admin/GestaoUsuarios.vue'
import Relatorios from '~/components/admin/Relatorios.vue'
import Monitoramento from '~/components/admin/Monitoramento.vue'
import BackupConfig from '~/components/admin/BackupConfig.vue'

</script>


<style scoped>
.admin-container {
  max-width: 1100px;
  margin: 36px auto;
  padding: 0 18px;
}
.admin-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 26px;
}
.logout-btn {
  background: #f66a0a;
  color: #fff;
  border: none;
  border-radius: 8px;
  padding: 10px 24px;
  font-weight: bold;
  cursor: pointer;
}
.admin-menu {
  display: flex;
  gap: 18px;
  margin-bottom: 32px;
}
.admin-menu button {
  background: #eee;
  border: none;
  border-radius: 8px;
  padding: 10px 20px;
  font-weight: 500;
  cursor: pointer;
  transition: background 0.2s;
}
.admin-menu button.active {
  background: #f66a0a;
  color: #fff;
}
.admin-section {
  background: #fff;
  border-radius: 14px;
  box-shadow: 0 2px 12px #0001;
  padding: 30px 24px;
  min-height: 320px;
}
</style>
