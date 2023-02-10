<template>
    <div class="main">
        <div class="title-container">
            <h1>{{ message }}</h1>
        </div>
        <div class="form-container">
            <form @submit="getPokemon">
                <div class="search-container">
                    <input type="text" v-model="name_pokemon" placeholder="Digite o nome do pokemon">
                    <button class="btn-search"><img src="../assets/search.svg" alt=""></button>
                </div>
            </form>
        </div>
        <div class="list-container">
            <ul v-for='item in pokemon' v-bind:key='item.id'>
                <li class="item-list-principal"> 
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
    .main{
        display: flex;
        align-items: center;
        flex-direction: column;
        justify-content: center;
        width: 100%;
        height: 90vh;
    }

    .title-container{
        width: 70%;
        margin-bottom: 50px;
    }
    .title-container h1{
        font-size: 1.875rem;
        color: #E83838;
    }

    .form-container{
        width: 70%;
    }
    form{
        width: 100%;
    }
    .search-container{
        width: 100%;
        height: 50px;
        display: flex;
        align-items: center;
        justify-content: space-between;
        border-radius: 30px;
    }
    .search-container input{
        padding-left: 15px;
        border: 1px solid #0066ff;
        border-radius: 15px 0 0 15px;
        width: 80%;
        height: 100%;
    }
    .search-container input:focus{
        border: 0.0938rem solid #071780;
        outline: none;
    }
    .btn-search{
        border: 1px solid #0066ff;
        height: 100%;
        border-radius: 0 15px 15px 0;
        width: 20%;
        background: #3192dc;
        transition: .5s;
    }
    .btn-search img{
        width: 1.125rem;
        height: 1.125rem;
    }
    .btn-search:hover{
        border: 0.0938rem solid #071780;
        cursor: pointer;
    }

    .list-container{
        width: 70%;
        margin-top: 50px;
    }

    .list-container ul{
        
        list-style-type: none;
        display: flex;
        align-items: center;
        overflow-x: auto;
        height: 300px;
    }

    .list-container li{
        margin-left: 20px;
        min-width: 150px;
        display: flex;
        flex-direction: column;
        align-items: center;
        justify-content: center;
        border-radius: 20px;
        box-shadow: 0px 2px 8px #0066ff;
        height: 250px;
        padding: 10px;
    }

    .list-container li:last-child{
        margin-right: 20px;
    }
    .list-container li img{
        width: 8.125rem;
    }

    .list-container li:hover{
        transform: scale(1.1);
        transition: all 0.7s ease 0s;
    }



</style>