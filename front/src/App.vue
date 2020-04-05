<template>
    <div class="container">
        <h1>Pokemon</h1>
        <PokemonList :imageUrl="imageUrl" :apiUrl="apiUrl" @setPokemonUrl="setPokemonUrl" />
        <PokemonDetail v-if="showDetail" :pokemonUrl="pokemonUrl" :imageUrl="imageUrl" @closeDetail="closeDetail" />
    </div>
</template>

<script>
import PokemonSearch from '@/components/PokemonSearch';
import PokemonList from '@/components/PokemonList';
import PokemonDetail from '@/components/PokemonDetail';

export default {
    data() {
        return {
            imageUrl: 'https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/',
            apiUrl: 'https://pokeapi.co/api/v2/pokemon',
            pokemonUrl: '',
            showDetail: false
        };
    },
    methods: {
        setPokemonUrl(url) {
            this.pokemonUrl = url;
            this.showDetail = true;
        },
        closeDetail() {
            this.pokemonUrl = '';
            this.showDetail = false;
        }
    },
    components: {
        PokemonSearch,
        PokemonList,
        PokemonDetail
    }
};
</script>

<style>
@import url('https://fonts.googleapis.com/css?family=Acme');

body {
    margin: 0;
}
.container {
    display: flex;
    justify-content: center;
    align-items: center;
    flex-direction: column;
    padding: 10px;
    width: calc(100% - 20px);
    min-height: calc(100vh - 20px);
    background: radial-gradient(#156f99, #0a2e50);
    font-size: 1rem;
    font-weight: normal;
    font-family: 'Acme';
}
h1 {
    color: #fff;
}
</style>
