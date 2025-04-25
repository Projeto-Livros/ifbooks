<script setup>
  import { FontAwesomeIcon } from "@fortawesome/vue-fontawesome";
  import { ref, computed, onMounted } from 'vue'

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
const livro = ref([
  {
    titulo: '1984',
    autor: `George Orwell`,
    descricao: 'Num futuro distópico, o mundo é controlado por um regime totalitário liderado pelo Grande Irmão. Winston Smith trabalha para o governo, mas começa a questionar o sistema opressor e busca liberdade. O livro mostra como a vigilância e a manipulação da verdade podem destruir a individualidade.',
    imagem: new URL('@/assets/images/1984.jpg', import.meta.url).href
  },
  {
    titulo: `Conectadas`,
    autor: `Clara Alves`,
    descricao: `Um romance contemporâneo brasileiro sobre duas garotas, Raíssa e Ayla, que se conhecem e se apaixonam através de um jogo online. A história fala de amizade, descoberta pessoal e amor LGBT+, tudo de um jeito leve, fofo e muito próximo da realidade dos jovens de hoje.` ,
    imagem: new URL('@/assets/images/conectadas.jpg', import.meta.url).href
  },
  {
    titulo: 'Carrie, A Estranha',
    autor: `Stephen King`,
    descricao: 'Carrie é uma adolescente tímida e atormentada pelos colegas e pela mãe fanática religiosa. Ela descobre que tem poderes telecinéticos e, após uma humilhação cruel no baile da escola, perde o controle e causa uma tragédia.',
    imagem: new URL('@/assets/images/carrie_a_estranha.jpg', import.meta.url).href
  },
  {
    titulo: `Os Sete Maridos de Evelyn Hugo`,
    autor: `Taylor Jenkins Reid`,
    descricao: `Evelyn Hugo, uma lendária estrela de Hollywood, finalmente decide contar a verdadeira história de sua vida: seus amores, seus segredos e seus sete casamentos. É uma narrativa emocionante sobre fama, ambição, paixão e identidade, cheia de reviravoltas e momentos intensos.` ,
    imagem: new URL('@/assets/images/os_sete_maridos_de_evelyn_hugo.jpg', import.meta.url).href
  },
  {
    titulo: `A Noite Passada no Telegraph Club`,
    autor: `Melinda Lo`,
    descricao: `Ambientado nos anos 1950, Lily é uma jovem chinesa-americana que descobre sua sexualidade quando conhece Kath em um clube LGBT secreto. O livro mostra o medo, os riscos e a coragem de viver um amor proibido naquela época.`,
    imagem: new URL('@/assets/images/a_noite_passada_no_telegraph_club.jpg', import.meta.url).href
  },
  {
    titulo: `It: A Coisa`,
    autor: `Stephen King`,
    descricao: `Um grupo de amigos enfrenta um ser maligno que assume a forma de seus piores medos, geralmente aparecendo como o palhaço Pennywise. Eles lutam contra a criatura quando crianças e, depois, precisam enfrentá-la novamente como adultos.` ,
    imagem: new URL('@/assets/images/it_a_coisa.jpg', import.meta.url).href
  },
  {
    titulo: 'Revolução dos Bichos',
    autor: `George Orwell`,
    descricao: 'Animais de uma fazenda se rebelam contra os humanos e criam seu próprio sistema de governo. Com o tempo, os porcos tomam o poder e passam a agir como os antigos opressores, mostrando como ideais podem ser corrompidos.',
    imagem: new URL('@/assets/images/revolucao_dos_bichos.jpeg', import.meta.url).href
  },
  {
    titulo: 'As Cronicas de Narnia ',
    autor: `C.S. Lewis`,
    descricao: 'Uma coletânea de sete histórias que se passam no mundo mágico de Nárnia, onde animais falam, há bruxas, leões e batalhas épicas entre o bem e o mal. É uma fantasia cheia de aventura e simbolismo cristão.',
    imagem: new URL('@/assets/images/as_cronicas_de_narnia.jpg', import.meta.url).href
  },
  {
    titulo: 'Contato',
    autor: `Carl Sagan`,
    descricao: 'A cientista Ellie Arroway capta uma mensagem de uma civilização alienígena e lidera uma missão para fazer contato com eles. O livro mistura ciência, filosofia e religião, questionando o lugar da humanidade no universo.',
    imagem: new URL('@/assets/images/contato.jpg', import.meta.url).href
  },
  {
    titulo: 'Coraline',
    autor: `Neil Gaiman`,
    descricao: 'Coraline descobre uma porta secreta em sua casa que leva a um mundo paralelo, onde tudo parece melhor – até demais. Lá, sua "outra mãe" quer prendê-la para sempre. Coraline precisa ser corajosa para salvar a si mesma e sua família.',
    imagem: new URL('@/assets/images/coraline.jpg', import.meta.url).href
  }

])
const indiceAtual = ref(0)

const livroAtual = computed(() => livro.value[indiceAtual.value])

function proximoLivro() {
  indiceAtual.value = (indiceAtual.value + 1) % livro.value.length
}

function voltarLivro() {
  indiceAtual.value =
    (indiceAtual.value - 1 + livros.value.length) % livros.value.length
}

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
onMounted(() => {
  setInterval(proximoLivro, 5000)
})
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
    <h2>Recomendados</h2>

    <div class="livro-container">
      <div class="livro-info">
        <h3>{{ livroAtual.titulo }}</h3>
        <h4>por {{ livroAtual.autor }}</h4>
        <p>{{ livroAtual.descricao }}</p>
      </div>

      <img
        :src="livroAtual.imagem"
        :alt="livroAtual.titulo"
        class="capa"
      />
    </div>

    <div class="botoes">
      <button @click="voltarLivro">Anterior</button>
      <button @click="proximoLivro">Próximo</button>
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




