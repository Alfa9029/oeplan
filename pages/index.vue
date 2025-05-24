<template>
  <div class="kanban-container">
    <header class="kanban-header">
      <h1>Painel de Tarefas</h1>
      <button class="new-task-btn" @click="abrirModalCriar = true">+ Nova Tarefa</button>
    </header>
    <div class="kanban-board">
      <div class="kanban-column" v-for="status in statusList" :key="status.value">
        <h2>{{ status.label }}</h2>
        <div class="kanban-tasks">
          <div
            class="task-card"
            v-for="task in tarefasPorStatus(status.value)"
            :key="task.id"
            @click="abrirDetalhes(task)"
          >
            <div class="task-title">{{ task.titulo }}</div>
            <div class="task-tags">
              <span v-for="tag in task.tags" :key="tag" class="tag">{{ tag }}</span>
            </div>
            <div class="task-meta">
              <span>{{ task.responsavel }}</span>
              <span>{{ task.dataCriacao }}</span>
            </div>
          </div>
        </div>
      </div>
    </div>
    <!-- Modal de Nova Tarefa -->
    <div v-if="abrirModalCriar" class="modal-bg">
      <div class="modal">
        <h3>Nova Tarefa</h3>
        <form @submit.prevent="criarTarefa">
          <input v-model="novaTarefa.titulo" placeholder="Título" required maxlength="60" />
          <textarea v-model="novaTarefa.descricao" placeholder="Descrição" maxlength="255"></textarea>
          <input v-model="novaTarefa.responsavel" placeholder="Responsável (e-mail)" required type="email" />
          <input v-model="novaTarefa.tagsStr" placeholder="Tags (separe por vírgula)" />
          <select v-model="novaTarefa.status">
            <option v-for="status in statusList" :value="status.value" :key="status.value">{{ status.label }}</option>
          </select>
          <button type="submit">Salvar</button>
          <button type="button" @click="abrirModalCriar = false">Cancelar</button>
        </form>
      </div>
    </div>
    <!-- Modal de Detalhes -->
    <div v-if="tarefaSelecionada" class="modal-bg">
      <div class="modal">
        <h3>{{ tarefaSelecionada.titulo }}</h3>
        <p>{{ tarefaSelecionada.descricao }}</p>
        <div><strong>Responsável:</strong> {{ tarefaSelecionada.responsavel }}</div>
        <div><strong>Data:</strong> {{ tarefaSelecionada.dataCriacao }}</div>
        <div class="task-tags">
          <span v-for="tag in tarefaSelecionada.tags" :key="tag" class="tag">{{ tag }}</span>
        </div>
        <label>Status:
          <select v-model="tarefaSelecionada.status" @change="atualizarStatusTarefa">
            <option v-for="status in statusList" :value="status.value" :key="status.value">{{ status.label }}</option>
          </select>
        </label>
        <div class="modal-actions">
          <button @click="removerTarefa(tarefaSelecionada.id)">Excluir</button>
          <button @click="fecharDetalhes">Fechar</button>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue'
const statusList = [
  { value: 'todo', label: 'To Do' },
  { value: 'inprogress', label: 'In Progress' },
  { value: 'inreview', label: 'In Review' }
]
const tarefas = ref([
  {
    id: 1,
    titulo: 'Exemplo de Tarefa',
    descricao: 'Detalhes da tarefa...',
    responsavel: 'prof@escola.com',
    status: 'todo',
    dataCriacao: '2025-05-23',
    tags: ['importante']
  }
])
const novaTarefa = ref({
  titulo: '',
  descricao: '',
  responsavel: '',
  status: 'todo',
  tagsStr: ''
})
const abrirModalCriar = ref(false)
const tarefaSelecionada = ref(null)
function tarefasPorStatus(status) {
  return tarefas.value.filter((t) => t.status === status)
}
function criarTarefa() {
  if (!novaTarefa.value.titulo || !novaTarefa.value.responsavel) return
  tarefas.value.push({
    id: Date.now(),
    titulo: novaTarefa.value.titulo,
    descricao: novaTarefa.value.descricao,
    responsavel: novaTarefa.value.responsavel,
    status: novaTarefa.value.status,
    dataCriacao: new Date().toISOString().split('T')[0],
    tags: novaTarefa.value.tagsStr.split(',').map((t) => t.trim()).filter(Boolean)
  })
  novaTarefa.value.titulo = ''
  novaTarefa.value.descricao = ''
  novaTarefa.value.responsavel = ''
  novaTarefa.value.status = 'todo'
  novaTarefa.value.tagsStr = ''
  abrirModalCriar.value = false
}
function abrirDetalhes(task) {
  tarefaSelecionada.value = { ...task }
}
function fecharDetalhes() {
  tarefaSelecionada.value = null
}
function removerTarefa(id) {
  tarefas.value = tarefas.value.filter((t) => t.id !== id)
  fecharDetalhes()
}
function atualizarStatusTarefa() {
  const idx = tarefas.value.findIndex((t) => t.id === tarefaSelecionada.value.id)
  if (idx >= 0) {
    tarefas.value[idx].status = tarefaSelecionada.value.status
  }
}
</script>

<style scoped>
.kanban-container {
  background: var(--bg-main);
  color: var(--text-main);
}
.kanban-column {
  background: var(--card-bg);
}
.new-task-btn {
  background: var(--primary);
  color: #fff;
}
.kanban-board {
  display: flex;
  gap: 28px;
}
.kanban-column {
  background: #f8fafc;
  border-radius: 14px;
  flex: 1;
  min-width: 240px;
  padding: 22px 16px;
  box-shadow: 0 2px 12px #0001;
}
.kanban-column h2 {
  font-size: 1.3rem;
  margin-bottom: 18px;
  color: #f66a0a;
}
.kanban-tasks {
  display: flex;
  flex-direction: column;
  gap: 16px;
}
.task-card {
  background: #fff;
  border-radius: 10px;
  box-shadow: 0 2px 8px #0001;
  padding: 16px;
  cursor: pointer;
  transition: box-shadow 0.2s, transform 0.12s;
}
.task-card:hover {
  box-shadow: 0 4px 18px #f66a0a22;
  transform: scale(1.025);
}
.task-title {
  font-weight: bold;
  font-size: 1.1rem;
  margin-bottom: 8px;
}
.task-meta {
  font-size: 0.94rem;
  color: #888;
  display: flex;
  justify-content: space-between;
  margin-top: 6px;
}
.task-tags {
  margin: 8px 0;
}
.tag {
  background: #f66a0a22;
  color: #f66a0a;
  font-size: 0.82rem;
  padding: 3px 10px;
  border-radius: 12px;
  margin-right: 6px;
}
.modal-bg {
  position: fixed;
  top: 0; left: 0;
  width: 100vw; height: 100vh;
  background: #0006;
  display: flex;
  align-items: center;
  justify-content: center;
  z-index: 10;
}
.modal {
  background: #fff;
  padding: 36px 30px;
  border-radius: 16px;
  box-shadow: 0 2px 24px #0004;
  max-width: 400px;
  width: 96%;
}
.modal-actions {
  margin-top: 18px;
  display: flex;
  justify-content: flex-end;
  gap: 16px;
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
