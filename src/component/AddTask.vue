<template>
  <div class="text-dark card" style="margin-left: 316px; max-width: 500px;">
        <div class="card-header">
            <h2>Add Task</h2>
        </div>
        <form @submit.prevent="handleAdd">
            <div>
                <label for="title">Title:</label>
                <input v-model="addTask.title" type="text" id="title" required placeholder="New Task..">
            </div>
            <div>
                <label for="title">Category:</label>
                <select v-model="addTask.category" class="form-select" >
                    <option selected>--Select Category--</option>
                    <option value="backlog">Backlog</option>
                    <option value="todo">Todo</option>
                    <option value="doing">Doing</option>
                    <option value="done">Done</option>
                </select>
            </div>

            <div style="margin-top: 5px;">
                <button class="btn btn-success" type="submit">Add task</button>
            </div>
        </form>
    </div>
</template>

<script>
export default {
    name: "AddTask",
    data() {
        return {
            addData : {
                title: '',
                category: ''
            }
        }
    },
    methods: {
        handleAdd () {
            this.$emit("add", this.addData)
            console.log(this.addData)
        }
    }
}
</script>

<style>

</style>