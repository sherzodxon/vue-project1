<template>
    <tr>
        <th scope="row">{{ user.id }}</th>
        <td :class="user.favourite?'text-warning':'text-dark'">{{ user.name }}</td>
        <td>{{ user.username }}</td>
        <td class="text-primary">{{ user.email }}</td>
        <td>{{ user.address.street }}</td>
        <td>{{ user.address.city }}</td>
        <td>
            <ul class="list-inline m-0">
                <li class="list-inline-item">
                    <button class="btn rounded btn-sm " :class="user.favourite?'star-button-clicked':'star-button'"
                        @click="onFavourite">
                    </button>
                </li>
                <li class="list-inline-item">
                   
                    <button @click="handleEdit" class="btn btn-sm btn-success rounded" data-bs-toggle="modal" data-bs-target="#editModal" title="Edit">
                        
                        <svg xmlns="http://www.w3.org/2000/svg" width="14" height="14" fill="currentColor"
                            class="bi bi-pencil-fill" viewBox="0 0 16 16">
                            <path
                                d="M12.854.146a.5.5 0 0 0-.707 0L10.5 1.793 14.207 5.5l1.647-1.646a.5.5 0 0 0 0-.708l-3-3zm.646 6.061L9.793 2.5 3.293 9H3.5a.5.5 0 0 1 .5.5v.5h.5a.5.5 0 0 1 .5.5v.5h.5a.5.5 0 0 1 .5.5v.5h.5a.5.5 0 0 1 .5.5v.207l6.5-6.5zm-7.468 7.468A.5.5 0 0 1 6 13.5V13h-.5a.5.5 0 0 1-.5-.5V12h-.5a.5.5 0 0 1-.5-.5V11h-.5a.5.5 0 0 1-.5-.5V10h-.5a.499.499 0 0 1-.175-.032l-.179.178a.5.5 0 0 0-.11.168l-2 5a.5.5 0 0 0 .65.65l5-2a.5.5 0 0 0 .168-.11l.178-.178z" />
                        </svg>
                    </button>
                </li>
                <li class="list-inline-item">
                    <button @click="onDelete" class="btn btn-danger btn-sm rounded" title="Delete">
                        <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" fill="currentColor"
                            class="bi bi-trash-fill" viewBox="0 0 16 16">
                            <path
                                d="M2.5 1a1 1 0 0 0-1 1v1a1 1 0 0 0 1 1H3v9a2 2 0 0 0 2 2h6a2 2 0 0 0 2-2V4h.5a1 1 0 0 0 1-1V2a1 1 0 0 0-1-1H10a1 1 0 0 0-1-1H7a1 1 0 0 0-1 1H2.5zm3 4a.5.5 0 0 1 .5.5v7a.5.5 0 0 1-1 0v-7a.5.5 0 0 1 .5-.5zM8 5a.5.5 0 0 1 .5.5v7a.5.5 0 0 1-1 0v-7A.5.5 0 0 1 8 5zm3 .5v7a.5.5 0 0 1-1 0v-7a.5.5 0 0 1 1 0z" />
                        </svg>
                    </button>
                </li>
            </ul>
        </td>
    </tr>
</template>
<script>
import Edit from '../edit/Edit.vue';

    export default {
        props: {
            user: {
                type: Object,
                required: true
            },
            modal:{
                type:String
            }
        },
        methods: {
            onFavourite() {
                this.$emit('onFavourite', this.user.id)
            },
            onDelete() {
                this.$emit('onDelete', this.user.id)
            },
            handleEdit(e){
                 this.$emit('onEdit', this.user.id)
            }
        },
        components:{
    Edit,
}


    }
</script>
<style>
    .star-button {
        padding: 10px;
        background: url(../../image/star.svg) no-repeat center center;

    }

    .star-button-clicked {
        padding: 10px;
        background: url(../../image/star-fill.svg) no-repeat center center;
    }
   
</style>