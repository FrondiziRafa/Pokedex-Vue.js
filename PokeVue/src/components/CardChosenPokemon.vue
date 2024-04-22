<script setup>
const pokemon = defineProps([
    "name", 
    "img", 
    "loading", 
    "pokemonEvolution", 
    "game_indices", 
    "moves",
    "sprites"
])
    
</script>

<template>
<div 
    class="card text-center cardSelectedPokemon"
    >
    <img
    v-if="pokemon.name"
    :src="pokemon.img"
    height="200"
    class="card-img-top pt-3" 
    :alt="pokemon.name"
    >
    <img
    v-else
    src="../assets/pokemon-23.svg"
    height="150"
    class="card-img-top pt-3" 
    alt="???"
    >
    <div class="card-body">
        <h5 class="card-title">{{ pokemon.name || " escolha um Pokemon" }}</h5>
        <hr>
        <div class="row">
            <section class="col">
                <strong>Sprites:</strong>
                <ul>
                    <li 
                    v-for="(sprite, index) in sprites"
                    :key="index"
                    >
                     <img :src="sprite" alt="">
                    </li>
                </ul>
            </section>
            <section class="col">
                <strong>Evoluções</strong>
                <ul>
                    <span 
                    v-for="evolution in pokemonEvolution"
                    :key="evolution.species"
                    >{{ evolution.species['name'] }}</span>
                </ul>
                <!-- <strong>Game indices</strong> -->
                <!-- <ul class="pb-3">
                    <li 
                    
                    v-for="(item, index) in game_indices"
                    :key="index"
                    >{{ item.version.name }}</li>
                </ul> -->
                <!-- <strong>Movimentos</strong>
                <ul class="pb-3">
                    <li 
                    
                    v-for="(move, index) in moves"
                    :key="index"
                    >{{ .move.name}}</li>
                </ul> -->
            </section>
        </div>
    </div>
</div>
</template>


<style scoped>
.cardSelectedPokemon{
    height: 60vh;
    background: rgb(72, 63, 251);
    background: radial-gradient(circle, rgb(220, 194, 106, 0.6) 0%, rgba(244, 0, 0, 0.3)100%);
}

</style>