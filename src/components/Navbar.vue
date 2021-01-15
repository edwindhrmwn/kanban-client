<template>
  <nav class="navbar navbar-expand-lg navbar-dark bg-dark shadow">
            <div class="container-fluid d-flex justify-content-between">
              <a class="navbar-brand" href="#">Kanban App</a>
              <button class="btn btn-danger" @click="logout()" v-if="halaman === 'content'">Logout</button>
            </div>
  </nav>
</template>

<script>
export default {
  props:['halaman','checkAuth'],
  methods:{
    logout(){
      localStorage.removeItem('access_token')
      this.checkAuth()
    }
  }
}
</script>

<style>

</style>