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
:root {
    --yellow: #fcba03;
    --black: #222;
}

* {
    font-family: Arial, Helvetica, sans-serif;
    padding: 0;
    margin: 0;
    box-sizing: border-box;
}

.main-container {
    margin: 50px;
    min-height: 50vh;
}

h1 {
    text-align: center;
    font-size: 42px;
    margin-bottom: 30px;
    color: var(--black);
}
</style>
