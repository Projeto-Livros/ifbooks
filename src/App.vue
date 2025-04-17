<script setup>
  import {ref} from "vue";

</script>

<template>
  <div class="pagina">
  <header>
    <h1>IFBooks</h1>
    <div class="pesquisa">
      <input type="text" placeholder="Pesquisar...">
      <span class="fa-solid fa-magnifying-glass"></span>
    </div>
    <div class="abas">
    <ul>
      <li>
        <a href="">Termos</a>
      </li>
      <li>
        <a href="">Equipe</a>
      </li>
      <li>
        <a href="">Envio</a>
      </li>
      <li>
        <a href="">Devoluções</a>
      </li>
    </ul>
    </div>
    <ul class="icones">    
      <li>
        <a href=""><span class="fa-solid fa-cart-shopping"></span></a>
      </li>
      <li>
        <a href=""><span class="fa-solid fa-heart"></span></a>
      </li>
      <li>
        <a href=""><span class="fa-solid fa-user"></span></a>
      </li>
    </ul>
  </header>
  <div class="corpo">

  </div>
  </div>
</template>

<style scoped>
  header h1{
    font-size: x-large;
    margin: 1vw 0vw 1vw 5vw;
  }
  
</style>
