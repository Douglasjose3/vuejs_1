<script setup>
import { reactive } from 'vue';

// JAVASCRIPT
const estado = reactive({
  filtro: 'todas',
  tarefaTemp: '',
  tarefas: [
    {
      titulo: 'Estudar ES6',
      finalizada: false,
    },
    {
      titulo: 'Estudar trade',
      finalizada: false,
    },
    {
      titulo: 'Limpar a casa',
      finalizada: true,
    }
  ]
})

const getTarefasPendentes = () => {
  return estado.tarefas.filter(tarefa => !tarefa.finalizada);
}

const getTarefasFinalizadas = () => {
  return estado.tarefas.filter(tarefa => tarefa.finalizada);
}

const getTarefasFiltradas = () => {
  const { filtro } = estado;

  switch (filtro) {
    case 'Pendentes': 
      return getTarefasPendentes();
    case 'Finalizadas':
      return getTarefasFinalizadas();
    default:
      return estado.tarefas;
  }
}

const cadastraTarefa = () => {
  const tarefaNova = {
    titulo: estado.tarefaTemp,
    finalizada: false,
  }
  estado.tarefas.push(tarefaNova);
  estado.tarefaTemp = '';
}

</script>

<template> <!-- HTML -->
  <div class="container">
    <header class="p-5 mb-4 mt-5 bg-secondary text-light rounded-4">
      <h1>Minhas tarefas</h1>
      <p>Você possui {{ getTarefasPendentes().length }} tarefas pendentes</p>
    </header>
    
    <form @submit.prevent="cadastraTarefa">
      <div class="row">  <!-- row = linha -->
        <div class="col">
          <input :value="estado.tarefaTemp" @change="evento => estado.tarefaTemp = evento.target.value" required type="text" placeholder="Digite aqui a tarefa" class="form-control">
        </div>
        <div class="col-md-2">
          <button class="btn btn-primary" type="submit">Cadastrar</button>
        </div>
        <div class="col-md-2">
          <select @change="evento => estado.filtro = evento.target.value" class="form-control">
            <option value="Todas">Todas as tarefas</option>
            <option value="Pendentes">Tarefas pendentes</option>
            <option value="Finalizadas">Tarefas finalizadas</option>
          </select>
        </div>
      </div> 
    </form>
    
    <ul class="list-group mt-4">
      <li class="list-group-item" v-for="tarefa in getTarefasFiltradas()">
        <input @change="evento => tarefa.finalizada = evento.target.checked" :checked="tarefa.finalizada" :id="tarefa.titulo" type="checkbox">
        <label :class="{ done: tarefa.finalizada }" class="ms-3" :for="tarefa.titulo">{{ tarefa.titulo }}</label>
      </li>
    </ul>
  </div>
</template>

<style scoped> /* CSS */
  .done {
    text-decoration: line-through;
  }

</style>
