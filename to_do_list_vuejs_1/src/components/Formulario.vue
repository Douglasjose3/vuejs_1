<script setup>
    const props = defineProps(['cadastraTarefa', 'tarefaTemp', 'trocarFiltro', 'editaTarefaTemp']);
</script>

<template>
    <form @submit.prevent="props.cadastraTarefa">
        <div class="row"> <!-- row = linha -->
            <div class="col">
                <input :value="props.tarefaTemp" @change="props.editaTarefaTemp" required type="text" placeholder="Digite aqui a tarefa" class="form-control">
            </div>
            <div class="col-md-2">
                <button class="btn btn-primary" type="submit">Cadastrar</button>
            </div>
            <div class="col-md-2">
                <select @change="props.trocarFiltro" class="form-control">
                    <option value="Todas">Todas as tarefas</option>
                    <option value="Pendentes">Tarefas pendentes</option>
                    <option value="Finalizadas">Tarefas finalizadas</option>
                </select>
            </div>
        </div>
    </form>
</template>