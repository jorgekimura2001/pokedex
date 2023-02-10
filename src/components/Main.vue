<template>
    <div class="main">
        <div class="title-container">
            <h1>{{ message }}</h1>
        </div>
        <div class="form-container">
            <form @submit="getPokemon">
                <div>
                    <input type="text" v-model="name_pokemon" placeholder="Faça sua pesquisa">
                    <button>Pesquisar</button>
                </div>
            </form>
        </div>
        <div class="list-container">
            <ul>

            </ul>
        </div>
    </div>
</template>

<script>
export default {
    name: 'Main-Component',
    props: {
        message: String
    },
    data () {
        return {
            name_pokemon: null
        }
    },
    methods: {
        async getPokemon(e){

            e.preventDefault()
            const pokemon = this.name_pokemon.trim().toLowerCase()
            const req = await fetch(`https://pokeapi.co/api/v2/pokemon/${pokemon}`)
            const data = await req.json()
            console.log(data)

            console.log(typeof this.name_pokemon)
        },
    },
}
</script>

<style scoped>

</style>