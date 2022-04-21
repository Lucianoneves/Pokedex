<template>
  <div id="app">
  <div class ="column is-half is-offset-one-quarter">
  <img src="./assets/vueeee.jpeg">
  <hr>
  <h4 class="is-size-4"> Pokedex</h4>
  <input type ="text" name="" id="" placeholder="buscar pokemon pelo nome" v-model="busca" class="input is-rounded" >
  <button class="button is-medium  is-primary" id="buscaBtn" @click="buscar">Buscar</button>
    <div v-for="(poke,index) in filterPokemons" :key="poke.url">
    <Pokemon :name="poke.name" :url="poke.url" :num="index+1"/>
  </div>
  </div>
</div>
</template>

<script>
import axios from 'axios';
// eslint-disable-next-line no-unused-vars
import Pokemon from './components/Pokemon.vue';
export default {
  name: 'App',
  data(){
    return {
     pokemons: [],
     filterPokemons: [],
     busca: ''
    }
  },
  created: function(){
    axios.get("https://pokeapi.co/api/v2/pokemon?limit=151&offset=0").then(res => {
      console.log("Pegou a lista de pokemom");
      this.pokemons = res.data.results;
      this.filterPokemons = res.data.result;
    })

  },
  components:{
    // eslint-disable-next-line vue/no-unused-components
    Pokemon
  },
  methods:{
    buscar: function(){
      this.filterPokemons = this.pokemons;
      if(this.busca == '' || this.busca == ''){
        this.filterPokemons = this.pokemons;
      }else{
        this.filterPokemons = this.pokemons.filter(pokemon => pokemon.name == this.busca);

    }
    }
  },
  computed: {
    /*
    resultadoBusca: function(){
      if(this.busca == '' || this.busca == ''){
        return this.pokemons;

      }else{
        return this.pokemons.filter(pokemon => pokemon.name == this.busca);
      }
    }*/
  }

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
  background-color: rgb(215, 232, 250);
}

#buscaBtn{
  margin-top: 2%;


}
</style>
