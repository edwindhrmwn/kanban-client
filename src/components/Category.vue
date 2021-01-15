<template>
    <div class="col-md-3">
        <div class="bg-secondary rounded p-2">
            <h5 class="text-light">{{name}}</h5>
            <draggable class="list-group" :list="currentTasks" group="tasks">
                <Task v-for="task in currentTasks" :key="task.id" :task="task" :data="{name,baseUrl}" :getKanbans="getKanbans" :notif="notif"></Task>
            </draggable>
            <p style="font-size:14px; color:white;" class="mt-1" data-bs-toggle="modal" :data-bs-target="id_Add">
                    <i class="bi-plus"></i> Add Task
            </p>

            <AddTask class="modal fade" :id="idAdd" tabindex="-1" aria-labelledby="exampleModalLabel" aria-hidden="true" :data="{name,baseUrl}" :getKanbans="getKanbans" :notif="notif"></AddTask>
        </div>
    </div>
</template>

<script>
import Task from '../components/Task'
import AddTask from '../components/AddTask'
import draggable from 'vuedraggable'
export default {
    components:{
        Task,
        AddTask,
        draggable
    },
    props:['name','tasks','baseUrl','getKanbans','notif'],
    data(){
        return{
            idAdd:'add'+this.name,
            id_Add:'#add'+this.name,
            arr: this.currentTasks
        }
    },
    methods:{

    },
    computed: {
        currentTasks: function(){
            this.arr = this.tasks.filter(task => task.category === this.name)
            return this.arr
        }
    }

}
</script>

<style scoped>
    p:hover{
        cursor: pointer;
    }
</style>>