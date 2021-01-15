<template>
  <div class="row">
    <Category v-for="category in categories" :key="category" :name="category" :tasks="dataTask" :baseUrl="baseUrl" :getKanbans="getKanbans" :notif="notif"></Category>
  </div>
</template>

<script>
import axios from 'axios'
import Category from '../components/Category'

export default {
  components:{
    Category
  },
  props:['baseUrl','checkAuth','notif'],
  data(){
    return {
      categories: ['Backlog','Product','Development','Done'],
      dataTask: []
    }
  },
  methods:{
    getKanbans(){
      axios({
          method: 'GET',
          url: this.baseUrl+'kanban',
          headers:{
            access_token: localStorage.access_token
          }
      })
      .then(response=>{
          console.log(">>>>ini content get kanban");
          // console.log(response.data);
          this.dataTask = response.data
      })
      .catch(err=>{
          console.log(err);
      })
    },
  },
  created(){
    this.getKanbans()
  }
}
</script>
<style>
  
</style>