<template>
  <div class="groups-container">
    <header class="groups-header">
      <h1>Meus Grupos</h1>
      <button class="new-group-btn" @click="abrirModalGrupo = true">+ Novo Grupo</button>
    </header>
    <div class="groups-list">
      <div class="group-card" v-for="grupo in grupos" :key="grupo.id">
        <h3>{{ grupo.titulo }}</h3>
        <p>{{ grupo.descricao }}</p>
        <div class="group-info">
          <span>Categoria: {{ grupo.categoria }}</span>
          <span>Visibilidade: 
            <select v-model="grupo.visibilidade" @change="atualizarVisibilidade(grupo)">
              <option value="publica">Pública</option>
              <option value="privada">Privada</option>
              <option value="restrita">Restrita</option>
            </select>
          </span>
        </div>
        <div class="group-participants">
          <strong>Participantes:</strong>
          <span v-for="p in grupo.participantes" :key="p">{{ p }}</span>
        </div>
        <div class="group-actions">
          <button @click="abrirEditarGrupo(grupo)">Editar</button>
          <button @click="removerGrupo(grupo.id)">Excluir</button>
          <button @click="verTarefas(grupo.id)">Ver Tarefas</button>
        </div>
      </div>
      <div v-if="grupos.length === 0" class="sem-grupos">Nenhum grupo encontrado.</div>
    </div>
    <!-- Modal de Novo/Editar Grupo -->
    <div v-if="abrirModalGrupo" class="modal-bg">
      <div class="modal">
        <h3>{{ editandoGrupo ? 'Editar Grupo' : 'Novo Grupo' }}</h3>
        <form @submit.prevent="salvarGrupo">
          <input v-model="grupoForm.titulo" placeholder="Título" required maxlength="60" />
          <textarea v-model="grupoForm.descricao" placeholder="Descrição" maxlength="255"></textarea>
          <input v-model="grupoForm.categoria" placeholder="Categoria" required maxlength="40" />
          <input v-model="grupoForm.participantesStr" placeholder="Participantes (e-mails separados por vírgula)" />
          <label>
            Visibilidade:
            <select v-model="grupoForm.visibilidade">
              <option value="publica">Pública</option>
              <option value="privada">Privada</option>
              <option value="restrita">Restrita</option>
            </select>
          </label>
          <button type="submit">Salvar</button>
          <button type="button" @click="fecharModalGrupo">Cancelar</button>
        </form>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue'
const grupos = ref([
  {
    id: 1,
    titulo: 'Grupo de Matemática',
    descricao: 'Docentes do departamento de matemática',
    categoria: 'Ensino Médio',
    participantes: ['prof1@escola.com', 'prof2@escola.com'],
    visibilidade: 'publica'
  }
])
const abrirModalGrupo = ref(false)
const editandoGrupo = ref(false)
const grupoEditandoId = ref(null)
const grupoForm = ref({
  titulo: '',
  descricao: '',
  categoria: '',
  participantesStr: '',
  visibilidade: 'publica'
})
function abrirEditarGrupo(grupo) {
  editandoGrupo.value = true
  grupoEditandoId.value = grupo.id
  grupoForm.value = {
    titulo: grupo.titulo,
    descricao: grupo.descricao,
    categoria: grupo.categoria,
    participantesStr: grupo.participantes.join(', '),
    visibilidade: grupo.visibilidade
  }
  abrirModalGrupo.value = true
}
function salvarGrupo() {
  const participantes = grupoForm.value.participantesStr.split(',').map(e => e.trim()).filter(Boolean)
  if (editandoGrupo.value) {
    const idx = grupos.value.findIndex(g => g.id === grupoEditandoId.value)
    if (idx !== -1) {
      grupos.value[idx] = {
        ...grupos.value[idx],
        titulo: grupoForm.value.titulo,
        descricao: grupoForm.value.descricao,
        categoria: grupoForm.value.categoria,
        participantes,
        visibilidade: grupoForm.value.visibilidade
      }
    }
  } else {
    grupos.value.push({
      id: Date.now(),
      titulo: grupoForm.value.titulo,
      descricao: grupoForm.value.descricao,
      categoria: grupoForm.value.categoria,
      participantes,
      visibilidade: grupoForm.value.visibilidade
    })
  }
  fecharModalGrupo()
}
function fecharModalGrupo() {
  abrirModalGrupo.value = false
  editandoGrupo.value = false
  grupoEditandoId.value = null
  grupoForm.value = {
    titulo: '',
    descricao: '',
    categoria: '',
    participantesStr: '',
    visibilidade: 'publica'
  }
}
function removerGrupo(id) {
  if (confirm('Deseja realmente excluir este grupo?')) {
    grupos.value = grupos.value.filter(g => g.id !== id)
  }
}
function atualizarVisibilidade(grupo) { }
function verTarefas(grupoId) {
  alert('Abrir tarefas do grupo ' + grupoId + '\nAqui você pode redirecionar para a tela de tarefas filtradas por grupo.')
}
</script>

<style scoped>
.groups-container {
  max-width: 950px;
  margin: 40px auto;
  padding: 0 14px;
}
.groups-header {
  display: flex;
  align-items: center;
  justify-content: space-between;
  margin-bottom: 28px;
}
.new-group-btn {
  padding: 10px 20px;
  background: #f66a0a;
  color: #fff;
  border-radius: 8px;
  border: none;
  font-weight: bold;
  cursor: pointer;
  transition: background 0.2s;
}
.groups-list {
  display: flex;
  flex-direction: column;
  gap: 22px;
}
.group-card {
  background: #fff;
  border-radius: 12px;
  box-shadow: 0 2px 8px #0001;
  padding: 24px 22px;
  position: relative;
}
.group-card h3 {
  margin-bottom: 4px;
  color: #f66a0a;
}
.group-info {
  margin-bottom: 8px;
  font-size: 0.97rem;
  color: #555;
  display: flex;
  gap: 18px;
}
.group-participants {
  font-size: 0.95rem;
  margin-bottom: 12px;
}
.group-participants span {
  background: #f66a0a22;
  color: #f66a0a;
  padding: 2px 9px;
  border-radius: 10px;
  margin-right: 6px;
  font-size: 0.89rem;
}
.group-actions {
  display: flex;
  gap: 12px;
}
.group-actions button {
  padding: 7px 16px;
  border-radius: 7px;
  border: none;
  background: #f66a0a;
  color: #fff;
  cursor: pointer;
  font-size: 0.99rem;
  transition: background 0.2s;
}
.group-actions button:nth-child(2) {
  background: #d33;
}
.group-actions button:nth-child(3) {
  background: #bbb;
  color: #222;
}
.sem-grupos {
  margin: 60px auto;
  color: #777;
  text-align: center;
}
.modal-bg {
  position: fixed;
  top: 0; left: 0;
  width: 100vw; height: 100vh;
  background: #0007;
  display: flex;
  align-items: center;
  justify-content: center;
  z-index: 10;
}
.modal {
  background: #fff;
  padding: 36px 28px;
  border-radius: 15px;
  box-shadow: 0 2px 24px #0004;
  max-width: 390px;
  width: 96%;
}
.modal input, .modal textarea, .modal select {
  width: 100%;
  padding: 10px;
  margin-bottom: 12px;
  border-radius: 7px;
  border: 1px solid #ddd;
  font-size: 15px;
}
.modal button {
  padding: 9px 22px;
  border-radius: 7px;
  border: none;
  margin-right: 8px;
  background: #f66a0a;
  color: #fff;
  cursor: pointer;
}
.modal button[type="button"] {
  background: #bbb;
  color: #222;
}
</style>
