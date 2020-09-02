<template>
  <div id="app">
    <div class="column is-half is-offset-one-quarter">
        <img src="./assets/guia.png">
        <hr>
        <h4 class="is-size-3">Pokedex</h4>

        <input type="text" class="input is-rounded" v-model="busca" placeholder="Buscar pokemon pelo nome">
        <button id="btn-buscar" class="button is-fullwidth is-success is-rounded" @click="buscar">Buscar</button>

        <div v-for="(poke, index) in filteredPokemons" :key="poke.url">
          <Pokemon :nome='poke.name' :url='poke.url' :num='index+1' />
        </div>
    </div>
    
  </div>
</template>

<script>
import axios from 'axios'
import Pokemon from './components/Pokemon'
export default {
  name: "App",
  data(){
    return {
      pokemons: [],
      filteredPokemons: [],
      busca: ''
    }
  },
  created: function(){
    axios.get("https://pokeapi.co/api/v2/pokemon?limit=151&offset=0").then(res =>{
      console.log('Pegou a lista de pokemons')
      this.pokemons = res.data.results
      this.filteredPokemons = res.data.results
      console.log(this.pokemons)
    })
  },
  components: {
    Pokemon
  },

  methods: {
    buscar: function(){
      this.filteredPokemons = this.pokemons
      if(this.busca == '' || !this.busca.trim()) {
        this.filteredPokemons = this.pokemons
      }
      else{
        this.filteredPokemons = this.pokemons.filter(Pokemon => Pokemon.name == this.busca)
      }
    }
  },

  computed: {

    // resultadoBusca: function(){
    //   if(this.busca == '' || !this.busca.trim()) {
    //     return this.pokemons
    //   }
    //   else{
    //     return this.pokemons.filter(pokemon => pokemon.name == this.busca)
    //   }
        
    // }
    
  }
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

#btn-buscar{
  margin-top: 2%;
}
</style>
