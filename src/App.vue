<script setup>
import {ref} from "vue";
import {useTaskStore} from "./stores/TaskStore"
import TaskDetails from "@/components/TaskDetails.vue";
import TaksForm from "@/components/TaksForm.vue";
import {storeToRefs} from "pinia";

const showAll = ref(true)

const taskStore = useTaskStore()

const { tasks, loading, favs, totalCount, favCount } = storeToRefs(taskStore)

taskStore.getTasks()

</script>

<template>
  <main>

    <header>
      <img src="./assets/pinia-logo.svg" alt="logo">
      <h1>Pinia Tasks</h1>
    </header>

    <div class="new-task-form">
      <TaksForm />
    </div>

    <nav class="filter">
      <button @click="showAll = true">All tasks</button>
      <button @click="showAll = false">Fav tasks</button>
    </nav>

    <div class="loading" v-if="loading">Loading tasks...</div>

    <div v-if="showAll" class="task-list">
      <p>Your have {{totalCount}} tasks left to do</p>
      <div v-for="task in tasks">
        <TaskDetails :task="task" :key="task.id"/>
      </div>
    </div>

    <div v-else class="task-list">
      <p>Your have {{favCount}} fav tasks left to do</p>
      <div v-for="task in favs">
        <TaskDetails :task="task" :key="task.id"/>
      </div>
    </div>
  <div class="button-container">
    <button @click="taskStore.$reset()">reset</button>
  </div>


  </main>
</template>

<style scoped>


</style>
