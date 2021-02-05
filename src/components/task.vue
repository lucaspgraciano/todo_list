<template>
    <div class="task" :class="stateClass" 
    @click="$emit('taskStateChanged', task)">
        <span @click="$emit('taskDeleted', task)" class="close">x</span>
        <p> {{ task.name }} </p>
    </div>
</template>

<script>
export default {
    props:{
        task: { type: Object, required: true }
    },
    computed: {
        stateClass() {
            return {
                pending: this.task.pending,
                done: !this.task.pending
            }
        }
    }
}
</script>

<style>
    .task{
        animation: task 4s;
        position: relative;
        box-sizing: border-box;
        width: 650px;
        height: 40px;
        border-radius: 5px;
        font-size: 1.1rem;
        font-weight: 300;
        user-select: none;
        display: flex;
        padding-left: 10px;
        margin-top: 5px;
        justify-content: left;
        cursor: pointer;
        align-items: center;
    }
    .pending{
        border-left: 12px solid #d00000aa;
        background-color: #ef233caa;
    }
    .done{
        color: #DDD;
        border-left: 12px solid #38b000;
        background-color: #006400aa;
        text-decoration: line-through;
    }
    .pending .close{
        background-color: #ef233caa;
    }
    .done .close{
        background-color: #006400aa;
    }
    .close{
        position: absolute;
        right: 10px;
        font-size: 0.9rem;
        font-weight: 600;
        height: 20px;
        width: 20px;
        border-radius: 10px;
        display: flex;
        justify-content: center;
    }
    @keyframes task {
        0%{width: 80px;}
        100%{width: 650px;}
    }
</style>
