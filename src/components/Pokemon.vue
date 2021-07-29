<template>
  <div class="container">
    <PokemonSearch 
      :apiUrl="apiUrl" 
      @setPokemonUrl="setPokemonUrl" />
      <h1>Liste des pokemon</h1>
    <PokemonList 
      :imageUrl="imageUrl" 
      :apiUrl="apiUrl"
      @setPokemonUrl="setPokemonUrl" />
    <!-- Si on clique sur 'details' -->
    <PokemonDetail 
      v-if="showDetail"
      :pokemonUrl="pokemonUrl"
      :imageUrl="imageUrl"
      :shinyUrl="shinyUrl"
      @closeDetail="closeDetail" />
  </div>
</template>

<script>
  import PokemonSearch from './PokemonSearch.vue';
  import PokemonList from './PokemonList.vue';
  import PokemonDetail from './PokemonDetail.vue';

  export default {
    data: () => {
      return {
        imageUrl: 'https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/',
        shinyUrl: 'https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/shiny/',
        apiUrl: 'https://pokeapi.co/api/v2/pokemon?limit=151',
        pokemonUrl: '',
        showDetail: false
      }
    },
    components: {
      PokemonSearch,
      PokemonList,
      PokemonDetail
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
    }
  }
</script>

<style lang="scss" scoped>
  @import url('https://fonts.googleapis.com/css2?family=Kanit&display=swap');

  .container {
    display: flex;
    justify-content: center;
    align-items: center;
    flex-direction: column;
    width: 100%;
    min-height: calc(100vh - 20px);
    background: rgb(46, 46, 46);
    font-family: 'Kanit';
    font-size: 1rem;
    font-weight: normal;
  }

  h1 { color: #efefef; }
</style>
