<template>
  <div id="app">
    <div class="column is-half is-offset-one-quarter">
      <h4 class="is-size-4">Pokedex</h4>
      <img src="./assets/pokebola.png" alt="pokebola" class="pokebola">
      <input class="input is-rounded" type="text" name="" id="" placeholder="Buscar Pokemon pelo nome" v-model="busca">
      <button class="button is-medium is-fullwidth is-success" id="buscaBtn" @click="buscar">Buscar</button>
      <div v-for="(poke,index) in filteredPokemon" :key="poke.url" >
        <Pokemon :num="index+1" :name="poke.name" :url="poke.url"/>
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios';
import Pokemon from './components/Pokemon';

export default {
  name: 'App',
  data(){
    return {
      pokemons: [],
      filteredPokemon: [],
      busca: '',
    }
  },
  created: function(){
    axios.get("https://pokeapi.co/api/v2/pokemon?limit=151&offset=0").then(res => {
      this.pokemons = res.data.results;
      this.filteredPokemon = res.data.results;
    })
  },
  methods:{
    buscar: function(){
      this.filteredPokemon = this.pokemons;
      if(this.busca == '' || this.busca == ''){  
        this.filteredPokemon = this.pokemons
      }else{  
        this.filteredPokemon = this.pokemons.filter(pokemon => pokemon.name == this.busca);
      }
    }
  },
  components:{
    Pokemon
  },
  // computed:{
  //   resultadoBusca: function(){
  //     if(this.busca == '' || this.busca == ''){
  //       return this.pokemons;
  //     }else{
  //       return this.pokemons.filter(pokemon => pokemon.name == this.busca);
  //     }
  //   }
  // }
}
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
#buscaBtn{
  margin-top: 1%;
}
.pokebola{
  width: 5%;
}
</style>
