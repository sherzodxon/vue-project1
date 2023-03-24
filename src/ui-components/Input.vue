<template >
    <input type="text" class="form-control mb-2 " :value="modelValue" @input="handleInput">
</template>
<script>
export default {
    methods:{
        handleInput(e){
            this.$emit('update:modelValue', e.target.value)
        }
    },
    props:{
        modelValue:[String , Number],
        required:true
    }
}
</script>
<style >
    
</style>