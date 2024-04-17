<script setup>
const pokemon = defineProps(["name", "urlSvg"])

</script>

<template>
    <div class="col-4">
        <div class="card mb-3 p-2">
            <p class="text-center">{{ pokemon.name }}</p>
            <img :src="urlSvg" class="card-img-top" alt="..."
            height="80"
            >
        </div>
    </div>
  
</template>


<style>

</style>