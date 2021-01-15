<template>
    <div>
        <h1><center>Register</center></h1>
        <form @submit.prevent="handleRegister">
            <div class="mb-3">
                <label for="exampleInputUsername1" class="form-label">User name</label>
                <input v-model="registerData.username" type="text" class="form-control" id="exampleInputUsername1" >
            </div>
            <div class="mb-3">
                <label for="exampleInputEmail1" class="form-label">Email address</label>
                <input v-model="registerData.email" type="email" class="form-control" id="exampleInputEmail1" >
            </div>
            <div class="mb-3">
                <label for="exampleInputPassword1" class="form-label">Password</label>
                <input v-model="registerData.password" type="password" class="form-control" id="exampleInputPassword1" >
            </div>
            <button type="submit" class="btn btn-primary">Submit</button>
        </form>
    </div>
</template>

<script>
export default {
    name: "RegisterForm",
    data() {
        return {
            registerData : {
                username: '',
                email: '',
                password: ''
            },
        }
    },
    methods: {
        handleRegister() {
            this.$emit("register", this.registerData)
            console.log(this.registerData)
            // this.registerData.username = ''
            // this.registerData.email = ''
            // this.registerData.password = ''
        },
    }
}
</script>

<style>

</style>