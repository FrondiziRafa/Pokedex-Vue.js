<script setup>
const pokemon = defineProps(["name", "img", "loading"])
    
</script>

<template>
<div 
    class="card text-center cardSelectedPokemon"
    >
    <img 
    :src="pokemon.img"
    height="200"
    class="card-img-top pt-3" 
    :alt="pokemon.name">
    <div class="card-body">
        <h5 class="card-title">{{ pokemon.name }}</h5>
        <hr>
        <div class="row">
            <section class="col">
                <strong>Sprites:</strong>
                <span>{{ pokemon.sprites }}</span>
            </section>
            <section class="col">
                <strong>Movimentos de Ataque:</strong>
                <span>{{ pokemon.moves }}</span>
            </section>
        </div>
    </div>
</div>
</template>


<style scoped>
.cardSelectedPokemon{
    background: rgb(72, 63, 251);
    background: radial-gradient(circle, rgb(220, 194, 106, 0.6) 0%, rgba(244, 0, 0, 0.3)100%);
}

</style>