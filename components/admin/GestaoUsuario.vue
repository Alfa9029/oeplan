<template>
  <div>
    <h2>Gestão de Usuários</h2>
    <table>
      <tr>
        <th>Nome</th>
        <th>E-mail</th>
        <th>Papel</th>
        <th>Ações</th>
      </tr>
      <tr v-for="user in users" :key="user.id">
        <td>{{ user.nome }}</td>
        <td>{{ user.email }}</td>
        <td>{{ user.papel }}</td>
        <td>
          <button @click="editarUser(user)">Editar</button>
          <button @click="removerUser(user.id)">Excluir</button>
        </td>
      </tr>
    </table>
  </div>
</template>
<script setup>
import { ref } from 'vue'
const users = ref([
  {id:1, nome:'Lucas', email:'lucas@escola.com', papel:'Professor'},
  {id:2, nome:'Ana', email:'ana@escola.com', papel:'Coordenador'}
])
function editarUser(user){ alert('Editar usuário: '+user.nome) }
function removerUser(id){ users.value = users.value.filter(u=>u.id!==id) }
</script>
<style scoped>
table { width:100%; margin-top:14px; border-collapse:collapse; }
th, td { border-bottom:1px solid #eee; padding:10px; }
button { margin-right:8px; background:#f66a0a; color:#fff; border:none; border-radius:5px; padding:6px 14px; cursor:pointer;}
button:last-child{background:#d33;}
</style>
