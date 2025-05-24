<template>
  <div>
    <h2>Relatórios</h2>
    <p>Aqui o admin pode gerar relatórios (ex: tarefas por docente, estatísticas).</p>
    <button @click="gerar">Gerar Relatório Exemplo</button>
    <div v-if="msg" class="msg">{{msg}}</div>
  </div>
</template>
<script setup>
import { ref } from 'vue'
const msg = ref('')
function gerar() {
  msg.value = 'Relatório gerado com sucesso!'
  setTimeout(()=>msg.value='',2000)
}
</script>
<style scoped>.msg{margin-top:16px;color:#2e8b57;}</style>
