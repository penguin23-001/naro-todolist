<script setup lang="ts">
import {ref} from 'vue'
interface Task {
    id: number
    name: string
    completed: boolean
}
const Tasks = ref<Task[]>([])
const newTaskName = ref<string>('')

const addTask = () => {
    Tasks.value?.push({ id:Tasks.value.length , name: newTaskName.value , completed: false })
    newTaskName.value = ''
}

const completeTask = (taskid: number) => {
    Tasks.value[taskid].completed = true
}

</script>

<template>
    <div>TaskList</div>
    <div>
        <label>
            タスク名
            <input v-model="newTaskName" style="text">
        </label>
        <button @click="addTask">
            追加
        </button>
    </div>
    <ul>
        <li v-for="task in Tasks " :key="task.id">
            <div>
                <button @click="completeTask(task.id)">
                    <div v-if="!task.completed">未</div>
                    <div v-if="task.completed">済</div>
                </button>
                {{ task.name }}
            </div>
        </li>
    </ul>
</template>

<style></style>