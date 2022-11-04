<template>
    <div class="container-fluid my-5" id="app">
        <h1 style="text-align: center">Parcial PNT2</h1>
        <br />
        <NavBar />
        <router-view> </router-view>
    </div>
</template>

<script>
import NavBar from "./components/NavBar.vue";

export default {
    name: "App",
    components: {
        NavBar,
    },
};
</script>

<style>
#app {
    font-family: Avenir, Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    color: #2c3e50;
    margin-top: 60px;
}
</style>
