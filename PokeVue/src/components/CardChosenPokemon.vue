<script setup>
const pokemon = defineProps(["name", "sprites"])
    
</script>

<template>
<div class="card text-center">
    <img src="..." class="card-img-top" alt="...">
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
                <span>30</span>
            </section>
        </div>
    </div>
</div>
</template>


<style>

</style>