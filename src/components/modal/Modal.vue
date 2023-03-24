<template>
 <div class="modal-wrapper">
  <button type="button" class="btn btn-primary" data-bs-toggle="modal" data-bs-target="#exampleModal">Add user</button>
  <div class="modal fade" id="exampleModal" tabindex="-1" aria-labelledby="exampleModalLabel" aria-hidden="true">
    <div class="modal-dialog">
      <div class="modal-content">
        <div class="modal-header">
          <h1 class="modal-title fs-5" id="exampleModalLabel">Modal title</h1>
          <button type="button" class="btn-close" data-bs-dismiss="modal" aria-label="Close"></button>
        </div>
        <form action="" class="form" @submit="addUser">
          <div class="modal-body">
            <Input v-model="name" placeholder="Name" />
            <Input v-model="username" placeholder="UserName" />
            <Input v-model="email" type="email"  placeholder="@Email" />
            <Input v-model="address.city" placeholder="city" />
            <Input v-model="address.street" placeholder="Street" />
          </div>
          <div class="modal-footer">
            <button  class="btn btn-warning">Add</button>
          </div>
        </form>

      </div>
    </div>
  </div>
 </div>
</template>
<script>
  import Input from '../../ui-components/Input.vue'

  export default {
    data() {
      return {
        id: 0,
        name: "",
        username: "",
        email: "",
        address: {
          street: "",
          city: ""
        },
        
      }
    },
    methods: {
      addUser(e) {
        e.preventDefault()
        const newUser = {
          id: ++this.id,
          name: this.name,
          username: this.username,
          email: this.email,
          favourite: false,
          address: {
            street: this.address.street,
            city: this.address.city
          }
        }
        if (this.name && this.email) {
          this.$emit("createUser", newUser)
          this.id = this.id
          this.name = ""
          this.username = ""
          this.email = ""
          this.address.street = ""
          this.address.city = ""
        }

      },
     
    },
    props: {
      count: {
        type: Number,
        required: true
      }
    },
    components: {
      Input
    },
    updated(){
      this.id=this.count
    }
  }
</script>
<style lang="">

</style>