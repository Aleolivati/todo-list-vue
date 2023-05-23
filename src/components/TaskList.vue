<script setup>
    const props = defineProps(['tasks']) ;

    // const filter = () => {
    //     console.log(filterLength)

    //     if (props.filterLength === 0) {
    //         true
    //     } else {
    //         false
    //     }
    // }
</script>

<template>
    <!-- <h3 v-if="props.getPendingTasks === 0">Parabéns! Você não tem tarefas pendentes! =D</h3>
    <h3 v-else-if="props.getFinishedTasks === 0">Parece que você não tem nenhuma tarefa completa =/</h3>
    <h3 v-else-if="props.getFinishedTasks + props.getPendingTasks === 0">Parece que você não tem mais nenhuma tarefa cadstrada =O <br /> Comece adicionando uma tarefa na caixa acima! ;)</h3> -->
    <ul class="list-group mt-4" v-for="task in tasks">
        <!-- <li v-if="task.length == 0">
            <h3>Parece que não existe nenhuma tarefa nesta categoria!</h3>
        </li> -->
        <li class="list-group-item">
            <input type="checkbox" :checked="task.finished" :id="task.title"
                @change="event => task.finished = event.target.checked">
            
            <label :for="task.title" class="ms-3" :class="{ done: task.finished }">{{ task.title }}</label>
        </li>
    </ul>
</template>

<style scoped>
.done {
    text-decoration: line-through;
}
</style>