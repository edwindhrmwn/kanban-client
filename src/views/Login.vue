<template>
    <div style="width:100%; height:100%;" class="d-flex justify-content-center align-items-center">
    <div id="login-form">
            <form class="login-form" @submit.prevent="login">
                <h1 class="h3 mb-3 fw-normal text-center">Login</h1>
                <input type="email" class="form-control mb-2" v-model="email" placeholder="Email address" autofocus>
                <input type="password" class="form-control mb-2" v-model="password" placeholder="Password">
                <button class="w-100 btn btn-lg btn-primary mb-2" type="submit" id="btn-login">Login</button><br>
                <a class="register-link link-blue" @click="methods.changePage('register')">don't have an account?</a><br>
                   <center>or</center>
                <!-- <div class="g-signin2 text-center" data-onsuccess="onSignIn"></div> -->
                <GoogleLogin :params="params" :renderParams="renderParams" :onSuccess="onSuccess"></GoogleLogin>

            </form> 
    </div>           
    </div>
</template>

<script>
import axios from 'axios'
import GoogleLogin from 'vue-google-login';
export default {
    components:{
        GoogleLogin
    },
    props:['methods','baseUrl','notif'],
    data(){
        return{
            email :'',
            password :'',
            params: {
                    client_id: "579612017479-opb137mfm09886nrbpeg50vmuocjb3du.apps.googleusercontent.com"
            },

            renderParams: {
                width: 250,
                height: 50,
                longtitle: true
            }
        }
    },
    methods:{
        login(){
            axios({
                method: 'POST',
                url: this.baseUrl+'login',
                data:{
                    email: this.email,
                    password: this.password
                }
            })
            .then(response=>{

                localStorage.access_token = response.data.access_token
                this.methods.checkAuth()

            })
            .catch(err=>{
                // console.log(err.response.data);
                this.notif(err.response.data.message)
            })
        },
        onSuccess(googleUser) {
            var id_token = googleUser.getAuthResponse().id_token;
            axios({
                method:'POST',
                url:this.baseUrl+'googleLogin',
                data:{token:id_token}
            })
            .then(response=>{
                localStorage.access_token = response.data.access_token
                this.methods.checkAuth()

            })
            .catch(err=>{
                console.log(err.response.data);
                this.notif(err.response.data.message)
            })
        }
    }
}
</script>

<style>
    #login-form{
        width: 30%;
    }
</style>