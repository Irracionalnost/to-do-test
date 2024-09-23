<script setup> 
import {useTemplateRef} from 'vue';
import { useStore } from '@/stores/store';
import { useEventListener } from '@vueuse/core'

const store = useStore();
const props = defineProps({
  id: Number,
  status: Boolean,
})

const input = useTemplateRef("input")
useEventListener(input, 'focusout', () => {
  input.value.disabled = true;
  localStorage.setItem('tasks', JSON.stringify(store.taskListArray));
})

const editTask = (id) => {
  input.value.disabled = false;
  store.taskListArray[id-1].isEdit = true;
  store.taskListArray[id-1].title = '';
  input.value.focus();
}

const taskDone = (id) => {
  store.taskListArray[id-1].status = !store.taskListArray[id-1].status;
  localStorage.setItem('tasks', JSON.stringify(store.taskListArray));
}

const deleteTask = (id) => {
  const findid = store.taskListArray.findIndex((item)=> item.id === id);
  store.taskListArray.splice(findid, 1);
  localStorage.setItem('tasks', JSON.stringify(store.taskListArray));
}
</script>

<template>
  <div class="task">
    <div class="title-task"> 
      <div @click="taskDone(id)" class="checkbox">
        <img v-if="status" src="/done.png" alt="">
      </div>
      <input ref="input"
      disabled
      v-model="store.taskListArray[id-1].title" 
      type="text" 
      :class="status ? 'done-task' : ''">
    </div>
    <div class="buttons">
      <button @click="editTask(id)" class="edit-button"> 
        <img src="/edit.png" alt="edit">
      </button>
      <button @click="deleteTask(id)" class="delete-button"> 
        <img src="/delete.png" alt="edit">
      </button>
    </div>
  </div>
</template>

<style scoped src="../assets/task.scss"></style>