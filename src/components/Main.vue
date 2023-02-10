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
            <ul v-for='item in pokemon' v-bind:key='item.id'>
                <li> 
                    <img :src='item.sprites.front_default' :alt='item.name'/>
                    <span>{{item.name}}</span>
                </li>
                <li v-if="generation1['red-blue'].front_default">
                   <img :src="generation1['red-blue'].front_default" :alt="`${item.name} - Geração 1`"> 
                   <span>{{item.name}} - Geração 1</span>
                </li>
                <li v-if="generation2['silver'].front_default">
                   <img :src="generation2['silver'].front_default" :alt="`${item.name} - Geração 2`"> 
                   <span>{{item.name}} - Geração 2</span>
                </li>
                <li v-if="generation3['ruby-sapphire'].front_default">
                   <img :src="generation3['ruby-sapphire'].front_default" :alt="`${item.name} Geração 3`"> 
                   <span>{{item.name}} - Geração 3</span>
                </li>
                <li v-if="generation4['heartgold-soulsilver'].front_default">
                   <img :src="generation4['heartgold-soulsilver'].front_default" :alt="`${item.name} Geração 4`"> 
                   <span>{{item.name}} - Geração 4</span>
                </li>
                <li v-if="generation5['black-white'].animated.front_default">
                   <img :src="generation5['black-white'].animated.front_default" :alt="`${item.name} Geração 5`"> 
                   <span>{{item.name}} - Geração 5</span>
                </li>
                <li v-if="generation6['omegaruby-alphasapphire'].front_default">
                   <img :src="generation6['omegaruby-alphasapphire'].front_default" :alt="`${item.name} Geração 6`"> 
                   <span>{{item.name}} - Geração 6</span>
                </li>
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
            name_pokemon: null,
            pokemon: [],
            generation1: [],
            generation2: [],
            generation3: [],
            generation4: [],
            generation5: [],
            generation6: [],
        }
    },
    methods: {
        async getPokemon(e){

            e.preventDefault()
            const pokemon = this.name_pokemon.trim().toLowerCase()
            const req = await fetch(`https://pokeapi.co/api/v2/pokemon/${pokemon}`)
            const data = await req.json()
            const {id, name, sprites} = data
            this.pokemon = [{
                id,
                name, 
                sprites
            }]
            this.generation1 = sprites.versions['generation-i']
            this.generation2 = sprites.versions['generation-ii']
            this.generation3 = sprites.versions['generation-iii']
            this.generation4 = sprites.versions['generation-iv']
            this.generation5 = sprites.versions['generation-v']
            this.generation6 = sprites.versions['generation-vi']
            
        },
    },
}
</script>

<style scoped>

</style>