<template>
    <footer id="footer">
        <p>Make Your Burger &copy; 2023</p>
    </footer>
</template>

<script>
export default {
    name: 'Footer',
}
</script>

<style scoped>
#footer {
    display: flex;
    bottom: 0;
    height: 200px;
    background-color: var(--black);
    border-top: 4px solid #111;
    color: var(--yellow);
    justify-content: center;
    align-items: center;
    width: 100%;
}
</style>