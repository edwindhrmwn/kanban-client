<template>
    <div class="container">
        <h1><center>Login</center></h1>
        <form @submit.prevent="login">
        <div class="mb-3">
            <label for="exampleInputEmail1" class="form-label">Email address</label>
            <input v-model = "loginData.email" type="email" class="form-control" id="exampleInputEmail1" aria-describedby="emailHelp">
        </div>
        <div class="mb-3">
            <label for="exampleInputPassword1" class="form-label">Password</label>
            <input v-model = "loginData.password" type="password" class="form-control" id="exampleInputPassword1">
        </div>
        <button type="submit" class="btn btn-primary">Submit</button>
        </form>
    </div>
</template>

<script>
export default {
    name: "LoginForm",
    data() {
        return {
            loginData: {
                email: '',
                password: ''
            },
        }
    },
    methods: {
        handle_login() {
            this.$emit("login", this.loginData)
            console.log(this.loginData)
        }
    }
}
</script>

<style>

</style>