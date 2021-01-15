<template>
    <div>
    <div class="modal-dialog">
        <div class="modal-content">
            <div class="modal-header">
                <h5 class="modal-title" id="exampleModalLabel">Add Task</h5>
                <a href="#" data-bs-dismiss="modal" aria-label="Close" class="bi-x" style="font-size:20px;"></a>
            </div>
            <div class="modal-body">
                <form @submit.prevent="addTask">
                    <input type="text" v-model="title" class="form-control" placeholder="title">
                </form>
            </div>
            <div class="modal-footer">
                <button type="button" class="btn btn-success" @click="addTask" data-bs-dismiss="modal">Add</button>
                <button type="button" class="btn btn-secondary" data-bs-dismiss="modal">Close</button>
            </div>
        </div>
    </div>
    </div>
</template>

<script>
import axios from 'axios'
export default {
    props:['data','getKanbans','notif'],
    data(){
        return {
            title :''
        }
    },
    methods:{
        addTask(){
            let data = {
                title : this.title,
                category : this.data.name
            }
            axios({
                method: 'POST',
                url: this.data.baseUrl+'kanban',
                headers:{
                    access_token: localStorage.access_token
                },
                data
            })
            .then(response=>{
                this.title = ''
                console.log("berhasil");
                this.getKanbans()
            })
            .catch(err=>{
                console.log(err);
                this.notif(err.response.data.message)
            })
            this.title = ''
        }
    }
}
</script>

<style>

</style>