<script setup>
  import {ref} from "vue";

</script>

<template>
<body>
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
</body>
</template>

<style scoped>

</style>
