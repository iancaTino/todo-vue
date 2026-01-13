<script setup>
import { reactive } from 'vue'

import Cabecalho from "./components/Cabecalho.vue"
import Formulario from './components/Formulario.vue'
import ListaDeTarefas from './components/ListaDeTarefas.vue'

const estado = reactive({
  filtro: 'todas',
  tarefaTemp: '',
  tarefas: [
    { titulo: 'Estudar ES6', finalizada: false },
    { titulo: 'Estudar SASS', finalizada: false },
    { titulo: 'Ir para a academia', finalizada: true },
  ]
})

const getTarefasPendentes = () =>
  estado.tarefas.filter(t => !t.finalizada)

const getTarefasFinalizadas = () =>
  estado.tarefas.filter(t => t.finalizada)

const getTarefasFiltradas = () => {
  switch (estado.filtro) {
    case 'pendentes':
      return getTarefasPendentes()
    case 'finalizadas':
      return getTarefasFinalizadas()
    default:
      return estado.tarefas
  }
}

const cadastraTarefa = () => {
  const titulo = estado.tarefaTemp.trim()
  if (!titulo) return

  estado.tarefas.push({
    titulo,
    finalizada: false
  })

  estado.tarefaTemp = ''
}

const toggleTarefa = ({ index, checked }) => {
  estado.tarefas[index].finalizada = checked
}
</script>

<template>
  <div class="container">
    <Cabecalho :tarefas-pendentes="getTarefasPendentes().length" />

    <Formulario :cadastra-tarefa="cadastraTarefa" :tarefa-temp="estado.tarefaTemp"
      :edita-tarefa-temp="e => estado.tarefaTemp = e.target.value"
      :trocar-filtro="e => estado.filtro = e.target.value" />

    <ListaDeTarefas :tarefas="getTarefasFiltradas()" @toggle="toggleTarefa" />
  </div>
</template>