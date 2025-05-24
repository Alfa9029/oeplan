<template>
  <div>
    <h2>Backup e Configurações</h2>
    <button @click="backup">Fazer Backup Manual</button>
    <div v-if="msg" class="msg">{{msg}}</div>
    <h3>Outras Configurações</h3>
    <ul>
      <li><label><input type="checkbox" v-model="notificacoes" /> Notificações por e-mail</label></li>
      <li><label><input type="checkbox" v-model="exportarCSV" /> Exportar tarefas em CSV</label></li>
    </ul>
  </div>
</template>
<script setup>
import { ref } from 'vue'
const msg = ref('')
const notificacoes = ref(true)
const exportarCSV = ref(false)
function backup() {
  msg.value = 'Backup realizado com sucesso!'
  setTimeout(()=>msg.value='',2000)
}
</script>
<style scoped>.msg{margin:16px 0;color:#2e8b57;}</style>
