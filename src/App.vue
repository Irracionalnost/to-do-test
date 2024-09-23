<script setup>
import TaskList from './components/TaskList.vue';
import { onMounted } from 'vue';
import { useStore } from '@/stores/store';
const store = useStore();

onMounted(() => {
  const arr = JSON.parse(localStorage.getItem('tasks'));
  if (arr.length > 0){
    console.log(1)
    store.taskListArray = arr;
  }
})

</script>

<template>
  <div>
    <h1>Список задач</h1>  
    <TaskList />
  </div>
</template>


