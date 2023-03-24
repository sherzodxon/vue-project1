<template >
    <div class="loader-wrapper">
        <span class="loader"></span>
    </div>
  
</template>
<script>
export default {
    
}
</script>
<style >
.loader-wrapper{
    width: 30px;
    height: 30px;
    position: absolute;
    left:calc(50% - 15px);
    margin-top: 10px;
}
.loader {
    width: 30px;
    height: 30px;
    margin:  0 auto;;
    border: 5px solid #fa7507;
    border-bottom-color: transparent;
    border-radius: 50%;
    display: inline-block;
    box-sizing: border-box;
    animation: rotation 1s linear infinite;
    }

    @keyframes rotation {
    0% {
        transform: rotate(0deg);
    }
    100% {
        transform: rotate(360deg);
    }
    } 
    
</style>