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
  <main>
    <div class="maisvendido">
      <h1>LIVRO MAIS VENDIDO DO MÊS</h1>
      <h2>Box Jurassic Park - Edição capa dura</h2>
      <h3>Este box reúne dois grandes clássicos de Michael Crichton: <br> o emblemático Jurassic Park e sua continuação, O Mundo Perdido.<br>
        Considerado pai do tecnothriller moderno, Crichton criou um universo <br> em que a genética foi capaz de clonar dinossauros extintos há milênios, <br> colocando-os em contato com seres humanos. Dessa ideia resultaram  <br> duas histórias eletrizantes, narradas com muita ação e suspense em uma <br> atmosfera tão perigosa quanto instigante.
        Os livros serviram de base para <br> o roteiro dos filmes dirigidos por Steven Spielberg, consagrando Jurassic <br> Park como um dos maiores blockbusters da história do cinema.
      </h3>
      <img  src="@/assets/jp.jpg" alt="jurassic">
    </div>
  </main>
</body>
</template>

<style scoped>

</style>
