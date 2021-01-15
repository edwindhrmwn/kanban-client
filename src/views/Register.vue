<template>
    <div style="width:100%; height:100%;" class="d-flex justify-content-center align-items-center">
    <div id="register-form">
            <form class="register-form" @submit.prevent="register">
                <h1 class="h3 mb-3 fw-normal text-center">Register</h1>

                <input type="email" v-model="email" class="form-control mb-2" placeholder="Email address" autofocus>

                <input type="password" v-model="password" class="form-control mb-2" placeholder="Password">

                <button class="w-100 btn btn-lg btn-primary mb-2" type="submit" id="btn-register">Register</button><br>
                <a class="login-link link-blue" @click="methods.changePage('login')">already have an account?</a><br>
            </form>
    </div>
    </div>
</template>

<script>
import axios from 'axios'
export default {
    props:['methods','baseUrl','notif'],
    data(){
        return{
            email : '',
            password : ''
        }
    },
    methods:{
        register(){
            axios({
                method: 'POST',
                url: this.baseUrl+'register',
                data:{
                    email: this.email,
                    password: this.password
                }
            })
            .then(response=>{
                this.methods.changePage('login')
            })
            .catch(err=>{
                // console.log(err);
                this.notif(err.response.data.message)
            })
        }
    }
}
</script>

<style scoped>
    #register-form{
        width: 30%;
    }
</style>>