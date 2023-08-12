<script setup lang="ts">
import {ref} from 'vue'
interface Task {
    id: number
    name: string
}
const Tasks = ref<Task[]>([])
const CompletedTasks = ref<Task[]>([])
const newTaskName = ref<string>('')

const addTask = () => {
    Tasks.value?.push({ id:Tasks.value.length , name: newTaskName.value })
    newTaskName.value = ''
}

const completeTask = (taskid: number) => {
    CompletedTasks.value.push(Tasks.value[taskid])
    Tasks.value.splice(taskid,1)
    for(var i = 0;i<Tasks.value.length;i++){
        Tasks.value[i].id = i
    }
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
    <div>タスク(未)</div>
    <ul>
        <li v-for="task in Tasks " :key="task.id">
            <div>
                <button @click="completeTask(task.id)">
                    未
                </button>
                {{ task.name }}
            </div>
        </li>
    </ul>
    <div>タスク(済)</div>
    <ul>
        <li v-for="task in CompletedTasks" :key="task.id">
            <div>
                <button>
                    済
                </button>
                {{ task.name }}
            </div>
        </li>
    </ul>
</template>

<style></style>