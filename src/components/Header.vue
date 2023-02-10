<template>
    <div class="header">
        <header>
            <h1>PokeDex</h1>
        </header>
        <img src='../assets/pokeball.svg' alt="">
    </div>
</template>

<script>
export default {
    name: 'Header-Component',
    props: {
        logo: String
    }
}
</script>

<style scoped>
    .header{
        width: 100%;
        display: flex;
        align-items: center;
        justify-content: space-between;
        background: #E83838;
        color: white;
        padding: 20px;
        margin-bottom: 20px;
    }
    .header img{
        width: 3.125rem;
        height: 3.125rem;
    }
</style>