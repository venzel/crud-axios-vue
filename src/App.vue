<template>
    <div id="app" class="container">
        <h1>HTTP com Axios</h1>
        <Crud />
    </div>
</template>

<script>
import Crud from './components/Crud.vue';

export default {
    components: { Crud },
    created() {},
};
</script>

<style>
#app {
    font-family: 'Avenir', Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    color: #2c3e50;
    font-size: 1.5rem;
}

#app h1 {
    text-align: center;
    margin: 50px;
}
</style>
