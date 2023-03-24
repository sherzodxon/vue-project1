<template>
    <div class="route-wrapper d-flex justify-content-center mt-3">
        <a class="btn text-info route--active" href="#/">Home</a>
        <a class="btn text-info route--active" href="#/about">About</a>
        <a class="btn text-info route--active" href="#/*">Contact</a>
    </div>

    <component :is="currentView" />
</template>
<script>
    import Home from './Home.vue';
    import About from '../pages/About.vue';
    import NotFound from '../pages/not-found/NotFound.vue'
    const routes = {
        '/': Home,
        '/about': About,
        '*':NotFound
    }
    export default {
        data() {
            return {
                currentPath: window.location.hash
            }
        },
        computed: {
            currentView() {
                return routes[this.currentPath.slice(1) || '/'] || NotFound
            }
        },
        mounted() {
            window.addEventListener('hashchange', () => {
                this.currentPath = window.location.hash
            })
        }
    }
</script>
<style>
.route--active{
    border-radius: 0;
   
}
.route--active:focus{
    border-bottom: 1px solid rgb(0, 174, 255);
}
</style>