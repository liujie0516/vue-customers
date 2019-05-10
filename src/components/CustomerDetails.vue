<template>
  <div class="details container">
      <router-link to="/" class="btn btn-default">返回</router-link>
  <h1 class="page-header">
      {{this.customer.name}}
      <span class="pull-right">
        <router-link class="btn btn-primary" v-bind:to="'/edit/'+customer.id">编辑</router-link>
        <button class="btn btn-danger" v-on:click="deleteCustomer(customer.id)">删除</button>
      </span>
  </h1>
  <ul class="list-group">
      <li class="list-group-item"><span class="glyphicon glyphicon-asterisk" ></span>{{customer.phone}}</li>
      <li class="list-group-item"><span class="glyphicon glyphicon-envelope"></span>{{customer.email}}</li>
  </ul>
  <ul class="list-group">
      <li class="list-group-item"><span class="glyphicon glyphicon-star-empty"></span>{{customer.education}}</li>
      <li class="list-group-item"><span class="glyphicon glyphicon-star-empty"></span>{{customer.graduationschool}}</li>
      <li class="list-group-item"><span class="glyphicon glyphicon-star-empty"></span>{{customer.profession}}</li>
      <li class="list-group-item"><span class="glyphicon glyphicon-star-empty"></span>{{customer.profile}}</li>     
  </ul>
  </div>
</template>

<script>
import axios from 'axios'
export default {
    name: 'customerDetails',
    data () {
        return {
        customer:""
            }
    },
    methods:{
        fetchCustomers(id){
            axios.get("http://localhost:3000/users/"+id).then(
                response=>{
                this.customer=response.data;
                }
            )
        },
        deleteCustomer(id){
            axios.delete("http://localhost:3000/users/"+id).then(
                response=>{
                   this.$router.push({path:'/',query:{alert:"用户信息删除成功！"}})  
                }
            )
        }
    },
    created(){
        this.fetchCustomers(this.$route.params.id)
    }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
