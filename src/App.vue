<script setup>
import {reactive} from 'vue' ;

const status = reactive ({
  filter:'all',
  tempTask: '',
  tasks: [
  {
      title: 'Estudar ES6',
      finished: false
    },
    {
      title: 'Estudar SASS',
      finished: false
    },
    {
      title: 'Ir na academia',
      finished: true
    }
  ]
})

const getPendingTasks = () => {
  return status.tasks.filter(task => !task.finished) ;
}

const getFinishedTasks = () => {
  return status.tasks.filter(task => task.finished) ;
}

const getFilterTasks = () => {
  const {filter} = status ;
  
  switch(filter) {
    case 'pending':
      return getPendingTasks() ;
    case 'finished':
      return getFinishedTasks() ;
    default:
      return status.tasks ;
  }
}

const addTask = () => {
  const newTask = {
    title: status.tempTask,
    finished: false
  }

  status.tasks.push(newTask) ;
  status.tempTask = '' ;
}

</script>



<template>
  <div class="container">
    <header class="p-5 mb-4 mt-4 bg-light rounded-3">
      <h1>Minhas tarefas</h1>
      <p>Você possui {{ getPendingTasks().length }} tarefas pendentes</p>
    </header>
    <form @submit.prevent="addTask()">
      <div class="row">
        <div class="col">
          <input required :value="status.tempTask" @change="event => status.tempTask = event.target.value" type="text" class="form-control" placeholder="Digite aqui a descrição da tarefa">
        </div>
        <div class="col-md-2">
          <button type="submit" class="btn btn-primary">Cadastrar</button>
        </div>
        <div class="col-md-2">
          <select class="form-control" @change="event => status.filter = event.target.value">
            <option value="all">Todas as tarefas</option>
            <option value="pending">Pendentes</option>
            <option value="finished">Finalizadas</option>
          </select>
        </div>
      </div>
    </form>
    <ul class="list-group mt-4">
      <li class="list-group-item" v-for="task in getFilterTasks()">
        <input type="checkbox" :checked="task.finished" :id="task.title" @change="event => task.finished = event.target.checked">
        <label :for="task.title" class="ms-3" :class="{done: task.finished}">{{ task.title }}</label>
      </li>
    </ul>
  </div>
</template>



<style scoped>
  .done {
    text-decoration: line-through;
  }
</style>
