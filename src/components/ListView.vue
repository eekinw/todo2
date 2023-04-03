<script setup>
const props = defineProps(["task"])
const emit = defineEmits(["complete", "remove"])
</script>


<template>
    <div class="mt-10 bg-yellow-200 p-3 rounded-lg">
        <ul class="flex justify-between items-center">
            <li :class="{ 'line-through': task.completed, 'italic text-xl': true}">{{ task.name }}</li>
            <div class="p-2 space-x-5">
                <button 
                class=" bg-green-400 p-2 rounded-lg cursor-pointer hover:scale-105"
                @click="emit('complete')"
                >Complete</button>
                <button 
                class=" bg-red-400 p-2 rounded-lg cursor-pointer hover:scale-105"
                @click="emit('remove')"
                >Remove</button>
            </div>

        </ul>
    </div>
</template>