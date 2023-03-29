<template>
    <main id="app">
        <Navbar :logo="logo_src" :alt="app_name" />
        <router-view />
        <Footer />
    </main>
</template>

<script>
import Navbar from './components/Navbar.vue'
import Footer from './components/Footer.vue'

export default {
    name: 'App',
    data() {
        return {
            logo_src: require('/src/assets/logo.png'),
            app_name: 'Make Your Burger',
        }
    },
    components: {
        Navbar,
        Footer,
    }
}
</script>

<style>
* {
    font-family: Arial, Helvetica, sans-serif;
    padding: 0;
    margin: 0;
    box-sizing: border-box;
}

.main-container {
    margin: 50px;
    min-height: 250px;
}

h1 {
    text-align: center;
    font-size: 42px;
    margin-bottom: 30px;
    color: #222;
}
</style>
