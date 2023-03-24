<template >
  <div class="container-xl border rounded mt-5 p-3 pb-5 border-ligth-subtle">
     <div class="header d-flex justify-content-between align-items-center">
      <h2 class="fs-3 text-warning text-center m-3">Vue practice</h2>
      <Modal :count="users.length" @createUser="addUser"/>
     <Edit v-if="edit.name" :user="edit" @editedUser="editedUser" />
     </div>
    <table class="table table-striped ">
      <Thead/>
      <tbody>
        <div v-if="loading" >
          <Loader />
      </div>
        <div v-else-if="!users.length" class="empty ml-auto">
          <p class="fs-3 text-center text-danger">Bo'sh</p>
        </div> 
        <Users  v-else v-for= "users in users"  :user="users" :key="users.id" @onFavourite="onFavourite" @onDelete="isDelete" @onEdit="isEditing"/>
       
      </tbody>
    
    </table>
  
  </div>
</template>
<script>

import AppInfo from '../components/app-info/AppInfo.vue';
import Thead from '../components/thead/Thead.vue'
import Users from '../components/users/Users.vue';
import Modal from '../components/modal/Modal.vue';
import Edit from '../components/edit/Edit.vue';
import Loader from '../ui-components/Loader.vue'
import About from '../pages/About.vue'
import axios from 'axios'
const routes= {
  '/about':About
}
export default {
    components: { AppInfo, Thead, Users, Modal, Edit ,Loader},
    data() {
      return {
        users: [
        ],
        edit:{},
        editIndex:0,
        loading:true
      }
      
    },
    methods:{
     async addUser(elements){
        try {
          const data = (await axios.post("https://jsonplaceholder.typicode.com/users",elements)).data
          console.log(data);
          this.users.push(elements)
        } catch (error) {
          alert("Xatolik!")
        }
       
      },
      onFavourite(c){
      this.users.map((el)=>{
        if (el.id === c) {
          el.favourite =!el.favourite
        }
        return el
      })
      },
      async isDelete(item){
        const findIndex = this.users.findIndex((el)=>el.id === item)
          this.users.splice(findIndex,1)
        try {
          const data = (await axios.delete(`https://jsonplaceholder.typicode.com/users/${item}`)).data
          console.log(data);
        } catch (error) {
          alert("Xatolik")
        }
       
      },
      isEditing(num){
        let find = this.users.find((el)=>el.id === num);
        this.edit=find
        this.editIndex=num
      },
      editedUser(data){
        const findIndex = this.users.findIndex((el)=>el.id === this.editIndex)
        this.users.splice(findIndex,1,data)
       
      },
      async fetchData(){
        try {
          const data= (await axios.get("https://jsonplaceholder.typicode.com/users")).data
        const users=data.map(el=>({
          id:el.id,
          name:el.name,
          username:el.username,
          email:el.email,
          favourite:false,
          address:{
            city:el.address.city,
            street:el.address.street
          }
        }))
        this.users=users;
        this.loading=false
        } catch (error) {
          alert("Serverda xatolik!")
        }
        
      }
    },
    mounted(){
     this.fetchData()
    }
    
  
      
}
</script>
<style>
  .empty{
    width: 100px;
    position: absolute;
    left: calc(50% - 50px);
  }
</style>