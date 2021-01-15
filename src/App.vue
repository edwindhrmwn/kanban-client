<template>
    <div style="height:98vh;">
        <Navbar :halaman="halaman" :checkAuth="checkAuth"></Navbar>
        <div class="container mt-3">
            <Login v-if="halaman === 'login'" :methods="{changePage,checkAuth}" :baseUrl="baseUrl" :notif="notif"></Login>
            <Register v-else-if="halaman === 'register'" :methods="{changePage,checkAuth}" :baseUrl="baseUrl" :notif="notif"></Register>
            <Content v-else-if="halaman === 'content'" :baseUrl="baseUrl" :checkAuth="checkAuth" :notif="notif"></Content>
        </div>
    </div>
</template>

<script>

import Navbar from './components/Navbar'
import Content from './views/Content'
import Login from './views/Login.vue'
import Register from './views/Register.vue'
import Swal from 'sweetalert2'

export default {
    components:{
        Navbar,
        Content,
        Login,
        Register
    },
    data(){
        return{
            halaman:'login',
            baseUrl: 'http://localhost:3000/'
        }
    },
    methods:{
        checkAuth(){
            if(localStorage.access_token){
                this.changePage('content')
            }else{
                this.changePage('login')
            }
        },
        changePage(page){
            console.log(page);
            this.halaman = page
        },
        notif(msg){
            Swal.fire({
                icon: 'error',
                title: 'Error',
                text: msg
            })
        }
    },
    created(){
        this.checkAuth()
    }
}
</script>

<style>
    .container{
        height: 90%;
    }
</style>