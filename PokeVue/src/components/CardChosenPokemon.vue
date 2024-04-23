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
<div class="card text-center cardSelectedPokemon">
    <img
    v-if="pokemon.name"
    :src="pokemon.img"
    class="card-img-top pt-3" 
    :alt="pokemon.name"
    >
    <img
    v-else
    src="../assets/pokemon-23.svg"
    class="card-img-top pt-3" 
    alt="???"
    >
    <div class="card-body">
        <h5 class="card-title">{{ pokemon.name || " escolha um Pokemon" }}</h5>
        <hr>
        <div class="">
            <div class="sprite-card ">
                <h3>Sprites:</h3>
                <ul class="">
                    <li 
                    v-for="(sprite, index) in sprites"
                    :key="index"
                    class="" 
                    >
                        <img :src="sprite" alt="">
                    </li>
                </ul>
            </div>
            <div class="attribute-card">
                <h3>Evoluções</h3>
                <h4
                v-for="(evolution, species) in pokemonEvolution"
                :key="species"
                >{{ evolution['name'] }}
                </h4>
            </div>
            <div class="attr">
                <div>
                    <h3>Games</h3>
                    <ul>
                        <li 
                        v-for="(game, index) in game_indices"
                        :key="index"
                        class="px-2 py-1"
                        >{{ game.version.name }}</li>
                    </ul>
                </div>
                <div>
                    <h3>Movimentos</h3>
                    <ul>
                        <li 
                        v-for="(move, index) in moves"
                        :key="index"
                        class=""
                        >{{ move.move.name}}</li>
                    </ul>
                </div>
            </div>
        </div>
    </div>
</div>
</template>


<style scoped>
.cardSelectedPokemon{
    height: 75vh;
    background: rgb(247, 247, 250);
    background: radial-gradient(circle, rgba(99, 206, 127, 0.6) 0%, rgba(249, 249, 249, 0.3)100%);
}

li {
    list-style: none;
}
.cardSelectedPokemon img{
    height:80px
}

.sprite-card {
    width: 100% !important;
}

.sprite-card ul {
    display: flex;
    flex-wrap: wrap;
    justify-content: space-between;

}

.sprite-card ul li {
    height: 70px;
    width: 70px;
}

.sprite-card ul li img {
    height: 70px;
    width: 70px;
}


.attr {
    display: flex;
    box-sizing:border-box;
    width: 100%;
    background: transparent;
    justify-content: space-between;
    padding: 10px;
}

.attr div  {
    width: 48%;
    height: 100%;
    border-radius:5px;
    box-sizing:border-box;
}

.attr div ul {
    overflow: scroll;
    overflow-x:hidden ;
    background: transparent;
    height:160px;

}

.attr div ul li {
    padding: 2px 5px;
    text-align: left;
}


@media (max-width: 600px) {
    
    .cardSelectedPokemon{
        height: 40vh;
        width:40%;
        margin:0 0 10px 0;
    }
    .cardSelectedPokemon img{
        height:100px
    }
}
</style>