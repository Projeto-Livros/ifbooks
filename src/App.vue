<script setup>
  import { FontAwesomeIcon } from "@fortawesome/vue-fontawesome";
  import {ref} from "vue";

  const paginaAtual = ref("home");

  function irParaCarrinho() {
    paginaAtual.value = "carrinho";
  }

  function irParaHome() {
    paginaAtual.value = "home";
  }



  const livros = ref([
  { titulo: 'Conectadas', genero: 'romance'},
  { titulo: 'Canção dos Ossos', genero: 'romance' },
  { titulo: 'Algumas garotas são assim', genero: 'romance' },
  { titulo: 'Sua Alteza Real', genero: 'romance' },
  { titulo: 'Lembre-se de Nós', genero: 'romance' },
  { titulo: 'Os Sete Maridos de Evelyn Hugo', genero: 'romance' },
  { titulo: 'A Noite Passada no Telegraph Club', genero: 'romance' },
  { titulo: 'Luzes do Norte', genero: 'romance' },
  { titulo: 'Sombras do Sul', genero: 'romance' },
  { titulo: 'Fogo & Estrelas', genero: 'romance' },
  { titulo: 'Gelo & Sombras', genero: 'romance' },
  { titulo: 'Box O Senhor dos Anéis', genero: 'fantasia' },
  { titulo: 'As Crônicas de Nárnia', genero: 'fantasia' },
  { titulo: 'Box Harry Potter', genero: 'fantasia' },
  { titulo: 'Cidade dos Ossos', genero: 'fantasia' },
  { titulo: 'O Nome do Vento', genero: 'fantasia' },
  { titulo: 'Eragon', genero: 'fantasia' },
  { titulo: 'A Canção do Sangue', genero: 'fantasia' },
  { titulo: 'Ciclo da Herança', genero: 'fantasia' },
  { titulo: '1984', genero: 'ficcao' },
  { titulo: 'Eu, Robô', genero: 'ficcao' },
  { titulo: 'Box Duna', genero: 'ficcao' },
  { titulo: 'A Guerra dos Mundos', genero: 'ficcao' },
  { titulo: 'Contato', genero: 'ficcao' },
  { titulo: 'Perdido em Marte', genero: 'ficcao' },
  { titulo: 'Estação 11', genero: 'ficcao' },
  { titulo: 'Box Jurassic Park', genero: 'ficcao' },
  { titulo: 'Divergente', genero: 'distopia' },
  { titulo: 'Jogos Vorazes', genero: 'distopia' },
  { titulo: 'Maze Runner', genero: 'distopia' },
  { titulo: 'Vox', genero: 'distopia' },
  { titulo: 'O Homem do Castelo Alto', genero: 'distopia' },
  { titulo: 'O Último Homem', genero: 'distopia' },
  { titulo: 'A Estrada', genero: 'distopia' },
  { titulo: 'Revolução dos Bichos', genero: 'distopia' },
  { titulo: 'It: A Coisa', genero: 'terror' },
  { titulo: 'O Iluminado', genero: 'terror' },
  { titulo: 'Carrie, A Estranha', genero: 'terror' },
  { titulo: 'O Exorcista', genero: 'terror' },
  { titulo: 'O Silêncio dos Inocentes', genero: 'terror' },
  { titulo: 'Coraline', genero: 'terror' },
  { titulo: 'O Grito', genero: 'terror' },
  { titulo: 'O Labirinto', genero: 'terror' },
])
const livrosFiltrados = ref([...livros.value])

function filtrar(genero) {
  if (genero === 'todos') {
    livrosFiltrados.value = [...livros.value]
  } else {
    livrosFiltrados.value = livros.value.filter(
      livro => livro.genero === genero
    )
  }
}
</script>
<template>
<body>
  <header>
    <h1>Livros & Letras</h1>
    <div class="pesquisa">
      <input type="text" placeholder="Pesquisar...">
      <FontAwesomeIcon icon="magnifying-glass" class="iconePesquisa"/>
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
        <a href="#" class="icon-btn" @click.prevent="irParaCarrinho"><FontAwesomeIcon icon="cart-shopping" /></a>
      </li>
      <li> |  </li>
      <li>
        <a href="/favoritos"><span class="fa-solid fa-heart"></span></a>
      </li>
      <li> |  </li>
      <li>
        <a href=""><span class="fa-solid fa-user"></span></a>
      </li>
    </ul>
  </header>

    <div v-if="paginaAtual === 'carrinho'" class="pagina-carrinho">
      <h2>🛒 Carrinho de Compras</h2>
      <p>Seu carrinho está vazio por enquanto.</p>
      <button @click="irParaHome">Voltar</button>
    </div>

  <main v-else>

    <div class="recomendados">
      <h1>RECOMENDADOS</h1>

    <div class="conteudo-jp">
    <div class="texto-jp">
      <h2>Box Jurassic Park - Edição capa dura</h2>
      <h3>Este box reúne dois grandes clássicos de Michael Crichton: <br> o emblemático Jurassic Park e sua continuação, O Mundo Perdido.<br>
        Considerado pai do tecnothriller moderno, Crichton criou um universo <br> em que a genética foi capaz de clonar dinossauros extintos há milênios, <br> colocando-os em contato com seres humanos. Dessa ideia resultaram  <br> duas histórias eletrizantes, narradas com muita ação e suspense em uma <br> atmosfera tão perigosa quanto instigante.
        Os livros serviram de base para <br> o roteiro dos filmes dirigidos por Steven Spielberg, consagrando Jurassic <br> Park como um dos maiores blockbusters da história do cinema.
      </h3>
    </div>
    <div class="imgjp"> <img src="@/assets/jp.jpg" alt="jurassic" /> </div>
    </div>

    </div>


    <div class="separador">
    <div class="generos">
      <button @click="filtrar('todos')">Todos</button>
      <button @click="filtrar('fantasia')">Fantasia</button>
      <button @click="filtrar('romance')">Romance</button>
      <button @click="filtrar('distopia')">Distopia</button>
      <button @click="filtrar('ficcao')">Ficção Científica</button>
      <button @click="filtrar('terror')">Terror</button>
    </div>
    </div>

    <div class="livros">
      <div
        v-for="livro in livrosFiltrados"
        :key="livro.titulo"
        class="livro"
      >
      <img :src="livro.imagem" :alt="livro.titulo" class="capa" />
        <p>{{ livro.titulo }} ({{ livro.genero }})</p>
      </div>
    </div>
  </main>
  <footer>

    <div class="redessociais">
      <span class="fa-brands fa-square-instagram"></span>
      <span class="fa-brands fa-square-facebook"></span>
      <span class="fa-brands fa-square-twitter"></span>
    </div>

    <div class="contato">
      <ul>
        <li><h4>CONTATO:</h4></li>
        <li>
          <span class="fa-solid fa-clock"> 9h ás 19h - Seg a Sex</span>
        </li>
        <li>
          <span class="fa-solid fa-envelope"> livros&letras@gmail.com</span>
        </li>
      </ul>
    </div>

    <div class="inscrevase">
      <input type="text" placeholder="Insira seu email">
      <button>Inscreva-se</button>
    </div>

    <div class="nome"> 
      <ul>
        <li>
          <h2>Livros</h2>
        </li>
        <li>
          <h2>&</h2>
        </li>
        <li>
          <h2>Letras</h2>
        </li>
      </ul>
    </div>

  </footer>
</body>
</template>
<style scoped>
</style>




