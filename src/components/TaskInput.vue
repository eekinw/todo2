<script setup>
import ListView from "../components/ListView.vue";
import { ref, computed } from "vue"

const tasks = ref([])
const newTask = ref("");

const addTask = () => {
    tasks.value.push({
        name: newTask.value,
        completed: false
    })

    newTask.value = "";
}

const taskCompleted = (index) => {
    tasks.value[index].completed = !tasks.value[index].completed;
}

const removeTask = (index) => {
    tasks.value.splice(index, 1);
}

const completedTasks = computed(() => tasks.value.filter(task => task.completed).length)

const charactersRemaining = computed(() => Math.max(0, 30 - newTask.value.trim().length))

const isCharacterLimitReached = computed(() => newTask.value.trim().length >= 30)

</script>


<template>
    <div class="mt-10">
        <p>Tasks Completed: {{ completedTasks }} / {{ tasks.length }}</p>
    </div>

    <div class="mt-5 space-x-6">
        <input 
        type="text" 
        class="border-2 border-sky-200 p-2 rounded-lg" 
        placeholder="Coding"
        v-model="newTask"
        @keyup.enter="addTask"
        >
        <button 
        class="border-2 border-black p-2 rounded-lg"
        @click="addTask"
        :disabled="isCharacterLimitReached"
        >Add</button>
    </div>

    <div class="mt-10">
        <p>Characters Left: {{ charactersRemaining }} / 30</p>
    </div>


    <ListView 
    v-for="(task, index) in tasks"
    :key="index"
    :task="task"
    @complete="taskCompleted(index)"
    @remove="removeTask(index)"
    />
    
</template>