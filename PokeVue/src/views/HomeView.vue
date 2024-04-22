<script setup>
import { onMounted, reactive, ref, computed } from 'vue';
import CardChosenPokemon from '../components/CardChosenPokemon.vue';
import PokemonList from '../components/PokemonList.vue';

let urlSvg = ref('https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/other/dream-world/');
let pokemonEvolution = reactive(ref());
let pokemons = reactive(ref());
let searchPokemonInput = ref('');
let selectedType = ref("")
let selectedSpecie = ref("")
let selectedPokemon = reactive(ref());
let pokemonTypes = reactive(ref());
let pokemonSpecies = reactive(ref())
let pokemonListTypes = reactive(ref())
let pokemonListSpecies = reactive(ref())
let game_indices = reactive(ref());

onMounted(() => {
  fetch("https://pokeapi.co/api/v2/pokemon?limit=1000&offset=0")
  .then(res => res.json())
  .then(res => pokemons.value = res.results)
  .then(console.log(pokemons))
  .then(allPokemonTypes())
  .then(allPokemonSpecies())
});

const filteredPokemons = computed((pokemon, pokemonListTypes) => {
  let filtered = pokemons.value
  if (searchPokemonInput.value) {
    return filtered.filter(pokemon => pokemon.name.toLowerCase().includes(searchPokemonInput.value.toLowerCase()));
  }
  else if(pokemonListTypes) {
    return filtered.filter(pokemon => pokemon.value.toLowerCase().includes(pokemonListTypes.value.toLocaleLowerCase()))
  }
  return pokemons.value;
});

const allPokemonTypes = async () => {
  try {
    const response = await fetch('https://pokeapi.co/api/v2/type');
    if (!response.ok) {
      throw new Error(`HTTP error! Status: ${response.status}`);
    }
    const data = await response.json();
    pokemonTypes.value = data.results;
    console.log(data);
  } catch (error) {
    console.error(error);
  }
};

const pokeType = async (selectedType) => {
    try {
      const response = await fetch(`https://pokeapi.co/api/v2/type/${selectedType}`);
      if(! response.ok) {
        throw new Error(`HTTP error! Status: ${response.status}`)
      }
      const data = await response.json()
      pokemonListTypes.value = data.results
      console.log(data) 

    } catch (error) {
      console.error(error);
  }
}

const pokeSpecie = async (selectedSpecie) => {
    try {
      const response = await fetch(`https://pokeapi.co/api/v2/pokemon-species/${selectedSpecie}`);
      if(! response.ok) {
        throw new Error(`HTTP error! Status: ${response.status}`)
      }
      const data = await response.json()
      pokemonListSpecies.value = data.results
      return data.name

    } catch (error) {
      console.error(error);
  }
}

const allPokemonSpecies = async () => {
    try {
      const response = await fetch('https://pokeapi.co/api/v2/pokemon-species');
      if (!response.ok) {
        throw new Error(`HTTP error! Status: ${response.status}`);
      }
      const data = await response.json();
      pokemonSpecies.value = data.results;
      console.log(pokemonSpecies.value);
    } catch (error) {
      console.error(error);
    
  }
};

const pokeEvolution = async () => {
  try{
    const evolutionResponse = await fetch(`https://pokeapi.co/api/v2/evolution-chain/${selectedPokemon.value.id}`);
      if (!evolutionResponse.ok) {
        throw new Error(`HTTP error! Status: ${evolutionResponse.status}`);
      }
      const evolutionData = await evolutionResponse.json();
      pokemonEvolution.value = evolutionData;
      console.log(evolutionData.chain.evolves_to[0])
    } 
  catch (error) {
      alert(error);
    }
}

const chosenPokemon = async (pokemon) => {
    try {
      const response = await fetch(pokemon.url);
      if (!response.ok) {
        throw new Error(`HTTP error! Status: ${response.status}`);
      }
      const pokemonData = await response.json();
      selectedPokemon.value = pokemonData;
      game_indices.value = pokemonData.game_indices;
      pokeEvolution()
  }
  catch (error) {
      alert(error);
    }
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
          :pokemonEvolution="pokemonEvolution?.chain.evolves_to[0]"
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
                hidden for="searchPokemonInput" 
                class="form-label"
                id="searchPokemonInput" 
                >
                Pesquisar...
              </label>
              <input
              v-model= "searchPokemonInput"
              type="text" 
              class="form-control" 
              id="exampleFormControlInput1" 
              placeholder="Pesquisar...">
              <select
                class="form-select"
                aria-label="Default select example"
                v-model="selectedType"
                @click="pokeType(selectedType)" 
                >
                  <option
                  v-for="(type, index) in pokemonTypes"
                  :key="index"
                  :value="type.name"
                  selected>Tipo {{ type.name }}</option>
              </select>
              
              <select
                class="form-select"
                aria-label="Default select example"
                v-model="selectedSpecie"
                @click="pokeSpecie(selectedSpecie)" 
                >
                  <option
                  v-for="(type, index) in pokemonSpecies"
                  :key="index"
                  :value="type.name"
                  selected>Tipo {{ type.name }}</option>
              </select>
              </div>
            <PokemonList 
              v-for="pokemon in filteredPokemons"
              :key="pokemon.name"
              :name="pokemon.name"
              :pokemonListTypes="pokemon.pokemonListTypes"
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
