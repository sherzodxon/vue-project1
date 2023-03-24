<template>
    <div class="modal fade modal-wrapper" id="editModal" tabindex="-1" aria-labelledby="editModalLabel" aria-hidden="true">
        <div class="modal-dialog">
            <div class="modal-content">
                <div class="modal-header">
                    <h1 class="modal-title fs-5" id="exampleModalLabel">Modal title</h1>
                    <button type="button" class="btn-close" data-bs-dismiss="modal" aria-label="Close"></button>
                </div>
                <form action="" class="form" @submit="editUser">
                    <div class="modal-body">
                        <Input :value="user.name" placeholder="Name" @input="name=$event.target.value" />
                        <Input :value="user.username" placeholder="UserName" @input="username=$event.target.value" />
                        <Input :value="user.email" type="email" placeholder="@Email" @input="email=$event.target.value" />
                        <Input :value="user.address.city" placeholder="city" @input="address.city=$event.target.value" />
                        <Input :value="user.address.street" placeholder="Street" @input="address.street=$event.target.value" />

                    </div>
                    <div class="modal-footer">
                        <button class="btn btn-warning">Edit</button>
                    </div>
                </form>

            </div>
        </div>
    </div>
</template>
<script>
    import Input from '../../ui-components/Input.vue'

    export default {
        components: {
            Input
        },
        props: {
            user: {
                type: Object,
                required: true
            }
        },
        data() {
            return {
                name: "",
                username: "",
                email: "",
                favourite: false,
                address: {
                    street: "",
                    city: ""
                }
            }
        },

        methods: {
            editUser(e) {
                e.preventDefault();
                let EditingUser = {
                    id: this.user.id,
                    name: this.name || this.user.name,
                    username: this.username || this.user.username,
                    email: this.email || this.user.email,
                    favourite: this.user.favourite,
                    address: {
                    street: this.address.street || this.user.address.street,
                    city: this.address.city || this.user.address.city
                    }
                }
                this.$emit("editedUser", EditingUser)
              
            }
        },
       
    }
</script>
<style>

</style>