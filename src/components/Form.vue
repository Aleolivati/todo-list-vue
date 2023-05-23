<script setup>
    const props = defineProps(['addTask', 'tempTask', 'editTempTask', 'filterChange']) ;
</script>

<template>
    <form @submit.prevent="props.addTask">
        <div class="row">
            <div class="col">
                <input required :value="props.tempTask" @change="props.editTempTask" type="text"
                    class="form-control" placeholder="Digite aqui a descrição da tarefa">
            </div>
            <div class="col-md-2">
                <button type="submit" class="btn btn-primary">Cadastrar</button>
            </div>
            <div class="col-md-2">
                <select class="form-control" @change="props.filterChange">
                    <option value="all">Todas as tarefas</option>
                    <option value="pending">Pendentes</option>
                    <option value="finished">Finalizadas</option>
                </select>
            </div>
        </div>
    </form>
</template>