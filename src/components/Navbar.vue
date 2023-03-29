<template>
    <nav id="nav">
        <router-link id="logo_url" to="/">
            <img :src="logo" :alt="alt" id="logo">
        </router-link>
        <router-link to="/">Fazer Pedido</router-link>
        <router-link to="/pedidos">Pedidos</router-link>
    </nav>
</template>

<style scoped>
#nav {
    background: #222;
    border: 0px 0px 4px 0px solid #111;
    padding: 15px 50px;
    display: flex;
    justify-content: flex-end;
    align-items: center;
}

#nav #logo_url {
    margin: auto;
    margin-left: 0;
}

#logo {
    width: 40px;
    height: 40px;
}

#nav a {
    color: #FCBA03;
    text-decoration: none;
    margin: 12px;
    transition: .5;
}

#nav a:hover {
    color: #fff;
}
</style>

<script>
export default {
    name: 'Navbar',
    props: ['logo', 'alt']
}
</script>