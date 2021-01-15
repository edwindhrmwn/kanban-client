<template>
    <div class="container">
        <nav-bar></nav-bar>
        <login-form v-if="page === 'login'" @login="login"></login-form>
        <RegisterForm v-if="page === 'register'" @register="register"></RegisterForm>
        <add-task v-if="page === 'add_task'" @add="add"></add-task>
        <home v-if="page === 'home'"></home>
    </div>
</template>

<script>
import axios from "axios"
import LoginForm from "./component/LoginForm"
import RegisterForm from "./component/RegisterForm"
import AddTask from "./component/AddTask"
import home from "./component/home"
import NavBar from "./component/NavBar"

export default {
    name: "App",
    data() {
        return {
            database_server: 'http://localhost:3000',
            page: 'home',
            tasks: [],
            categories: [],
            // addTask: {
            //     title: '',
            //     category: ''
            // },
        }
    },
    components: {
        LoginForm,
        RegisterForm,
        home,
        NavBar,
        AddTask
    },
    created() { 
        this.checkAuth()
    },
    methods: {
        changeTo(value) {
            this.page = value
        },
        checkAuth(){
            if (localStorage.access_token){
                this.readTasks()
                this.page = "home"
                this.user = localStorage.user
            } else {
                this.changeTo('add_task')
            }
        },
        login(value) {
            // res.send(value)
            axios({
                method: 'post',
                url: `${this.database_server}/login`,
                data: {
                    email: value.email,
                    password: value.password
                }
            })
            .then(response => {
                this.loginData.email =  '',
                this.loginData.password =  ''
                localStorage.setItem('access_token', res.data.access_token)
                localStorage.setItem('user', email)
                this.checkAuth()
                console.log('sukses')
            })
            .catch (err => {
                console.log(err)
            })
            // console.log(value)
        },
        register(value) {

            // console.log(value);
            axios({
                method: 'post',
                url: `${this.database_server}/register`,
                data: {
                    username: value.username,
                    email: value.email,
                    password: value.password
                }
            })
            .then(response => {
                console.log(response);
                // changeTo('login')
                this.page = 'login'
                console.log('sukses')
            })
            .catch(err => {
                console.log(err.response.data)
            })
        },
        add(value) {
            // console.log(this.addTask.title)
            // console.log(this.addTask.category)
            axios({
                method: `POST`,
                url: `${this.database_server}/task`,
                // headers: {
                //     access_token: localStorage.getItem('access_token')
                // },
                data: {
                    title: value.title,
                    category: value.category,
                }
            })
            .then(response => {
                console.log(response.data, '----------')
            })
            .catch(err => {
                console.log(err)
            })
        },
        readAllData() {
            axios({
                method: "GET",
                url: `${this.database_server}/task`,
            })
            .then(({data}) => {
                this.data
            })
            .catch(err => {
                console.log(err)
            })
        },
        delete(id) {
            axios({
                method: 'DELETE',
                url: `${this.baseUrl}/task/${id}`,
                headers: {
                    access_token: localStorage.getItem('access_token')
                }
            })
            .then(response => {
                console.log(response)
                this.checkAuth()
            })
            .catch(err => {
                console.log(err)
            })
        },
        edit(value){
            axios({
                method: 'PUT',
                url: `${this.database_server}/edit/${value.id}`,
                headers: {
                    access_token: localStorage.getItem('access_token')
                },
                data: {
                    title: this.value.title
                }
            })
            .then(response => {
                console.log('sukses');
                this.checkAuth()
            })
            .catch(err => {
                console.log(err);
            })
        },
        addCategory (value) {
            axios({
                method: 'POST',
                url: `${this.database_server}/category`,
                data: {
                    name: this.value.name
                }
            })
            .then(response => {
                console.log('sukses');
                this.checkAuth()
            })
            .catch(err => {
                console.log(err)
            })
        },
        readCategory() {
            axios({
                method: 'GET',
                url: `${this.database_server}/category`
            })
            .then(response => {
                this.categories = response.data
            })
            .catch(err => {
                console.log(err)
            })
        }

    }
}
</script>

<style>
</style>