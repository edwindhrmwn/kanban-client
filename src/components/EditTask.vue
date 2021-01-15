<template>
    <div>
    <div class="modal-dialog">
        <div class="modal-content">
            <div class="modal-header">
                <h5 class="modal-title" id="exampleModalLabel">Edit Task</h5>
                <a href="#" data-bs-dismiss="modal" aria-label="Close" class="bi-x" style="font-size:20px;"></a>
            </div>
            <div class="modal-body">
                <form @submit.prevent="updateTask(task.id)">
                    <input type="text" v-model="title" class="form-control" placeholder="title">
                    <div class="input-group mt-3 w-100">
                        <label class="input-group-text" for="inputGroupSelect01">Category</label>
                        <select class="form-select" id="inputGroupSelect01" v-model="category">
                            <option selected>Choose...</option>
                            <option value="Backlog">Backlog</option>
                            <option value="Product">Product</option>
                            <option value="Development">Development</option>
                            <option value="Done">Done</option>
                        </select>
                    </div>
                </form>
            </div>
            <div class="modal-footer">
                <button type="button" class="btn btn-success" data-bs-dismiss="modal" @click="updateTask(task.id)">Save</button>
                <button type="button" class="btn btn-secondary" data-bs-dismiss="modal">Close</button>
            </div>
        </div>
    </div>
    </div>
</template>

<script>
import axios from 'axios'
export default {
    props:['data','getKanbans','task','notif'],
    data(){
        return {
            title : this.task.title,
            category : ''
        }
    },
    methods:{
        updateTask(id){
            let data = {
                title : this.title,
                category : this.category
            }
            axios({
                method: 'PUT',
                url: this.data.baseUrl+'kanban/'+id,
                headers:{
                    access_token: localStorage.access_token
                },
                data
            })
            .then(response=>{
                console.log("berhasil");
                this.getKanbans()
            })
            .catch(err=>{
                // console.log(err.response);
                this.notif(err.response.data.message)
            })
        }
        
    },
    created(){
        // console.log(this.data,this.task);
    }
}
</script>

<style>

</style>