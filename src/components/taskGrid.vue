<template>
    <div class="taskGrid">
        <template>
           <Task v-for="(task, id) in tasks" :key="task.name" :task="task" 
                @taskDeleted="$emit('taskDeleted', id)"
                @taskStateChanged="$emit('taskStateChanged', id)" ></Task>
        </template>
    </div>
</template>

<script>
import Task from './task.vue'

export default {
    components: { Task },
    props: {
        tasks: {type: Array, required: true}
    }
}
</script>

<style>

</style>