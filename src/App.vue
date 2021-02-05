<template>
    <div id="app">
        <h1>Tarefas</h1>
        <newTask @taskAdded="addTask"/>
        <div v-show="tasks.length != 0">
            <taskProgress :progress="progress" />
            <div id="container">
                <taskGrid :tasks="tasks" @taskDeleted="deleteTask"
                                     @taskStateChanged="toggleTaskState"/>
            </div>
        </div>
 
    </div>
</template>

<script>
import taskProgress from './components/progressTask'
import newTask from './components/newTask.vue'
import taskGrid from './components/taskGrid.vue'

export default {
    components: { newTask, taskGrid, taskProgress },
    data(){
        return {
            tasks: [] 
        }
    },
    computed: {
        progress() {
            const total = this.tasks.length
            const done = this.tasks.filter(t => !t.pending).length
            return Math.round(done/total * 100) || 0
        }
    },
    methods: {
        addTask(task) {
			const sameName = t => t.name === task.name
			const reallyNew = this.tasks.filter(sameName).length == 0
			if(reallyNew) {
				this.tasks.push({
					name: task.name,
					pending: task.pending || true
				})
			}else{
                alert('Tarefa já cadastrada!')
            }
		},
        deleteTask(id){
            this.tasks.splice(id, 1)
        },
        toggleTaskState(id){
            this.tasks[id].pending = !this.tasks[id].pending
        }
    },
    watch: {
        tasks: {
            deep: true,
            handler() {
                localStorage.setItem('tasks', JSON.stringify(this.tasks))
            }
        }
    },
    created(){
        const json = localStorage.getItem('tasks')
        this.tasks = JSON.parse(json) || []
    }
}
</script>

<style>
body{
    font-family: 'Lato', sans-serif;
    background: linear-gradient(to right, #12c2e9, #c471ed, #f64f59);
    color:#fff;
}
#app {
    display: flex;
    flex: 1;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    height: 100%;
}
#app h1 {
    margin-bottom: 5px;
    font-weight: 300;
    font-size: 3rem;
	}
#container{
    animation: container 3s;
    background: linear-gradient(#f8f9fa,#dee2e6,#adb5bd);
    width: 800px;
    padding: 20px;
    color: #111;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    border-radius: 25px;
    margin:10px;
}
@keyframes container {
    0%{width: 250px;}
    100%{width: 800px;}
}
</style>
