<template>
  <div class="card mb-2" style="max-width: 16rem;">
    <div class="card-body text-secondary">
        <p class="card-text fw-bold">{{task.title}}</p>
        <div class="d-flex flex-row-reverse">
            <ul class=" d-flex flex-row-reverse">
                <li><a href="#" class="bi-trash text-secondary" @click="deleteTask(task.id)"></a></li>
                <li><a href="#" class="bi-pencil text-secondary" data-bs-toggle="modal" :data-bs-target="edit_Id"></a></li>
            </ul>
        </div>
    </div>

    <EditTask class="modal fade" :id="editId" tabindex="-1" aria-labelledby="exampleModalLabel" aria-hidden="true" :data="data" :task="task" :getKanbans="getKanbans" :notif="notif"></EditTask>
    
  </div>
</template>

<script>
import axios from 'axios'
import EditTask from '../components/EditTask'

export default {
    components:{
        EditTask
    },
    data(){
        return {
            editId : 'edit'+this.task.id,
            edit_Id : '#edit'+this.task.id
        }
    },
    props:['task','data','getKanbans','notif'],
    methods:{
        deleteTask(id){
            axios({
                method: 'DELETE',
                url: this.data.baseUrl+'kanban/'+id,
                headers:{
                    access_token: localStorage.access_token
                }
            })
            .then(response=>{
                console.log("berhasil");
                this.getKanbans()
            })
            .catch(err=>{
                console.log(err);
                this.notif(err.response.data.message)
            })
        
        }
    }
}
</script>

<style scoped>
    ul li{
        list-style: none;
        margin-right: 10px;
        line-height: 0;
    }
    a{
        font-size: 16px;
    }
</style>