<script setup>
import {ref} from 'vue'
import router from './router';

let num = ref(0)

</script>

<template>
  <!-- Navbar -->
  <nav  class="navbar navbar-expand-lg navbar-dark bg-primary">
  <div class="container-fluid">
    <a class="navbar-brand" href="#">
      <img width="48" height="48" src="https://img.icons8.com/fluency/48/pokeball.png" alt="pokeball"/>
      PokeVue
    </a>
    <button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#navbarNavDropdown" aria-controls="navbarNavDropdown" aria-expanded="false" aria-label="Toggle navigation">
      <span class="navbar-toggler-icon"></span>
    </button>
    <div class="collapse navbar-collapse" id="navbarNavDropdown">
      <ul class="navbar-nav">
        <li class="nav-item">
          <router-link class="nav-link" aria-current="page" to="/">Home</router-link>
        </li>
        <li class="nav-item">
          <router-link class="nav-link" to="about">Sobre</router-link>
        </li>
        <li class="nav-item dropdown">
          <a class="nav-link dropdown-toggle" href="#" role="button" data-bs-toggle="dropdown" aria-expanded="false">
            Idiomas
          </a>
          <ul class="dropdown-menu">
            <li>
                <a class="dropdown-item" href="#">
                  <img width="48" height="48" src="https://img.icons8.com/fluency/48/brazil-circular.png" alt="brazil-circular"/>
                  Português
              </a>
            </li>
            <li>
                <a class="dropdown-item" href="#">
                <img width="48" height="48" src="https://img.icons8.com/fluency/48/usa-circular.png" alt="usa-circular"/>
                English
              </a>
            </li>
            <li>
                <a class="dropdown-item" href="#">
                  <img width="48" height="48" src="https://img.icons8.com/color/48/spain2-circular.png" alt="spain2-circular"/>
                  Español 
              </a>
            </li>
          </ul>
        </li>
      </ul>
    </div>
  </div>
</nav>

<!-- Content -->

<div class="main">
  <router-view></router-view>
</div>

<!-- Footer -->

<footer class="bg-primary text-light">
  <div>
    {{ new Date().getFullYear() }}
  </div>
</footer>

</template>

<style>
  footer {
    position:fixed;
    bottom:0;
    width: 100%;
    display: flex;
    align-items: center;
    justify-content: center;
    height: 56px;
}
</style>