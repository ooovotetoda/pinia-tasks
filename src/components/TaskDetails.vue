<script setup>
import {useTaskStore} from "@/stores/TaskStore";

const props = defineProps({
  task: Object
})

const taskStore = useTaskStore()
</script>

<template>
<div class="task">
  <h3>{{task.title}}</h3>
  <div class="icons">
    <i class="material-symbols-outlined" @click="taskStore.deleteTask(task.id)">delete</i>
    <i
      class="material-symbols-outlined" @click="taskStore.toggleFav(task.id)"
      :class="{ active: task.isFav }"
    >favorite</i>
  </div>
</div>
</template>

<style scoped>

</style>