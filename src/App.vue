<script setup>
import {reactive} from 'vue' ;
import TaskList from './components/TaskList.vue';
import Form from './components/Form.vue';
import Header from './components/Header.vue';

const status = reactive ({
  filter:'all',
  tempTask: '',
  tempStatus: false,
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
      const getPendingTemp = getPendingTasks() ;
      // status.tempStatus = false ;

      // if (getPendingTemp.length == 0) {
      //   status.tempStatus = true ;
      // } else {
      //   status.tempStatus = false ;
      // }

      return getPendingTemp ;
      
    case 'finished':
    const getFinishedTemp = getFinishedTasks() ;
      // status.tempStatus = false ;

      // if (getFinishedTemp.length == 0) {
      //   status.tempStatus = true ;
      // } else {
      //   status.tempStatus = false ;
      // }

      return getFinishedTemp ;

    default:
      // status.tempStatus = false ;

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
    <Header :pending-tasks="getPendingTasks().length" />
    <Form :temp-task="status.tempTask" :edit-temp-task="event => status.tempTask = event.target.value" :add-task="addTask" :filter-change="event => status.filter = event.target.value" />
    <TaskList :tasks="getFilterTasks()"/>
  </div>
</template>




