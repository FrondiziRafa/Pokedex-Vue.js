<script setup>
const pokemon = defineProps(["name", "urlSvg"])

</script>

<template>
    <div class="col-4">
        <div class="card mb-3 p-2 cardList">
            <img :src="urlSvg" class="card-img-top" alt="name"
            height="80"
            >
            <p class="text-center">{{ name }}</p>
        </div>
    </div>
</template>


<style scoped>
.cardList {
    background: rgb(72, 63, 251);
    background: radial-gradient(circle, rgb(72, 63, 251, 0.5) 0%, rgba(70, 252, 244, 0.3)100%);
    cursor: pointer; 
}
.cardList:hover {
    background: rgb(72, 63, 251);
    background: radial-gradient(circle, rgb(72, 63, 251, 0.6) 0%, rgba(70, 252, 244, 0.2)100%);
}
.cardList img:hover {
    padding: .1rem;
}

</style>