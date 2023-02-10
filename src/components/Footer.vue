<template>
    <footer>
        <p>Desenvolvido por {{dev}} | © Todos os Direitos Reservados</p>
    </footer>
</template>

<script>
export default {
    name: 'Footer-Component',
    props: {
        dev: String
    }
}
</script>

<style scoped>
    footer{
        background: #E83838;
        color: white;
        height: 50px;
        display: flex;
        align-items: center;
        justify-content: center;
        font-size: 10px;
    }
</style>