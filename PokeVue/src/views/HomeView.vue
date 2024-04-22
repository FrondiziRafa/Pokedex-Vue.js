<script setup>
import { onMounted, reactive, ref, computed } from 'vue';
import CardChosenPokemon from '../components/CardChosenPokemon.vue';
import PokemonList from '../components/PokemonList.vue';

let urlSvg = ref('https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/other/dream-world/')
let pokemonEvolution = reactive(ref())
let pokemons = reactive(ref());
let searchPokemonInput = ref("")
let selectedPokemon = reactive(ref())
let pokemonTypes = reactive(ref())
let game_indices = reactive(ref())

onMounted(() => {
  fetch("https://pokeapi.co/api/v2/pokemon?limit=1000&offset=0")
  .then(res => res.json())
  .then(res => pokemons.value = res.results);
  })

const filteredPokemons = computed(() => {
  if(pokemons.value && searchPokemonInput.value ){
    return pokemons.value.filter(pokemon => pokemon.name.toLowerCase().includes(searchPokemonInput.value.toLocaleLowerCase()))
  }
  // console.log(pokemons.value)
  return pokemons.value;
})

const allPokemonTypes = async(pokemon, id) => {
  await fetch('https://pokeapi.co/api/v2/type')
  .then(res => res.json())
  .then(res => pokemonTypes.value = res)
  .then(console.log(pokemonTypes))
}

const chosenPokemon = async(pokemon, id) => {
  await fetch(pokemon.url)
  .then(res => res.json())
  .then(res => selectedPokemon.value = res)
  .then(console.log(selectedPokemon))
  .then(res => game_indices.value = res)
  .catch(err => alert(err))
  
  await fetch(`https://pokeapi.co/api/v2/pokemon-species/${selectedPokemon.value.id}`)
  .then(res => res.json())
  .then(res => pokemonEvolution.value = res)
  .then(allPokemonTypes())
  .catch(err => alert(err))
}

</script>

<template>
  <main>
    <div class="container text-body-secondary">
      <div class="row mt-5">
        <div class="col-sm-12 col-md-6">
          <CardChosenPokemon
          :name="selectedPokemon?.name"
          :img="selectedPokemon?.sprites.other.dream_world.front_default"
          :sprites="selectedPokemon?.sprites"
          :game_indices="selectedPokemon?.game_indices"
          :moves="selectedPokemon?.moves"
          />
        </div>
        <div 
          class="col-sm-12 col-md-6"
        >
          <div class="card card-list">
            <div class="card-body row">
              <div class="mb-3">
                <label 
                hidden for="searchPokemonInput" class="form-label">Email address
              </label>
              <select
                v-for="(index,type ) in pokemonTypes"
                :key="index"
                class="form-select"
                aria-label="Default select example"
                >
                <option selected>Tipo</option>
                <option value="1">{{type.results.name}}</option>
              </select>
                <input
                v-model= "searchPokemonInput"
                type="text" class="form-control" id="exampleFormControlInput1" placeholder="Pesquisar...">
              </div>
            <PokemonList 
              v-for="pokemon in filteredPokemons"
              :key="pokemon.name"
              :name="pokemon.name"
              :urlSvg ="urlSvg + pokemon.url.split('/')[6] + '.svg'"
              @click="chosenPokemon(pokemon)"
            />
            </div>
          </div>
        </div>
      </div>
    </div>
  </main>
</template>

<style scoped>
.card-list {
  max-height: 60vh;
  overflow-y: scroll;
  overflow-x: hidden;
}

</style>
