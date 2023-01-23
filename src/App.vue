<template>
  <main>

    <!-- heading -->
    <header>
      <img src="https://pinia.vuejs.org/logo.svg" alt="pinia logo">
      <h1> PINIA TODO LIST </h1>
    
    </header>
    <div class="new-task-form">
    <TaskForm />
  </div>
    <nav class="filter">
      <button @click="filter ='favs'"> Favourite</button>
      <button  @click="filter='all'"> All Tasks</button>
    </nav>

    <!-- <div class="loading" v-if="taskStore.loading">
      <h1> Loading </h1>
    </div> -->

    <div class="task-list" v-if="filter === 'all'">
      <p> Total Tasks : {{ taskStore.totalCount }} </p>

    <div v-for="task in taskStore.tasks" :key="task.id">
      <TaskDetails :task="task"/>
    </div>
    </div>

    <div class="task-list" v-if="filter ==='favs'">
      <p> Favourite Tasks: {{ taskStore.favCount }} </p>

    <div v-for="task in taskStore.favs" :key="task.id">
      <TaskDetails :task="task"/>
    </div>
    </div>


  </main>
</template>

<script>
    import {useTaskStore} from "./stores/TaskStore"
    import TaskDetails from "./components/TaskDetails.vue"
    import TaskForm from "./components/TaskForm.vue"
import { ref } from '@vue/reactivity'

  export default {
    components :{TaskDetails,TaskForm},
    setup(){
      const taskStore =useTaskStore()

      taskStore.getTask()
      const filter = ref('all')
    
    return {taskStore,filter}
  }
  }
</script>