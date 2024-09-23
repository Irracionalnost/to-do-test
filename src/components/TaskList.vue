<script setup>
import { useStore } from '@/stores/store';
const store = useStore();

import Task from "./Task.vue";

const addTask = () => {
    store.taskListArray.push({
        id: store.taskListArray.length + 1, 
        title: 'Новая задача', 
    })
    localStorage.setItem('tasks', JSON.stringify(store.taskListArray));
}
</script>

<template>
    <div class="to-do-block">
        <div class="button-container">
            <button @click="addTask" class="button-add">
                <img class="mr-1" src="/plus.png" alt="+">
                <span>Добавить новую задачу</span>
            </button>
        </div>
        <div class="task-container">
            <h2 v-if="store.taskListArray.length === 0">Пока задач нет.</h2>
            <Task v-for="item in store.taskListArray" :key="item.id" 
                :id="item.id"
                :status="item.status"
            />
        </div>
    </div>
    
</template>

<style scoped src="../assets/tasklist.scss"></style>