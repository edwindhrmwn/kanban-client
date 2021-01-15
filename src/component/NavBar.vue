<template>
    <nav class="navbar navbar-expand-lg navbar-light bg-light">
    <a class="navbar-brand">KANBAN</a>
    <button class="navbar-toggler" type="button" data-toggle="collapse" data-target="#navbarNav" aria-controls="navbarNav" aria-expanded="false" aria-label="Toggle navigation">
        <span class="navbar-toggler-icon"></span>
    </button>
    <div class="collapse navbar-collapse" id="navbarNav">
        <ul class="navbar-nav">
        <li class="nav-item active" v-show="page === 'register'">
            <a class="nav-link">Login</a>
        </li>
        <li class="nav-item" v-show="page === 'login'">
            <a class="nav-link" >Register</a>
        </li>
        <li class="nav-item" >
            <a class="nav-link">Logout</a>
        </li>
        <li class="nav-item" v-show="page !== 'register'">
            <a class="nav-link" v-show="page !== 'login'">add task</a>
        </li>
        </ul>
    </div>
    </nav>
</template>

<script>
export default {
    name: "NavBar",
    page: ''
}
</script>

<style>

</style>