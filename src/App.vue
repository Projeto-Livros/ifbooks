<script setup>
  import { FontAwesomeIcon } from "@fortawesome/vue-fontawesome";
  import { ref, computed, onMounted } from 'vue'

  const paginaAtual = ref("home");

  function irParaCarrinho() {
    paginaAtual.value = "carrinho";
  }

  function irParaFavoritos() {
    paginaAtual.value = "favoritos";
  }

  const emailUsuario = ref('');
  const inscrito = ref(false);

  function inscreverEmail() {
    if (emailUsuario.value.trim() !== '') {
      inscrito.value = true;
    }
  }


  function irParaHome() {
    paginaAtual.value = "home";
  }


  const carrinho = ref([]);
  const favoritos = ref([]);

  function adicionarAoCarrinho(livro) {
    if (!carrinho.value.includes(livro)) {
      carrinho.value.push(livro);
    }
  }

  function adicionarAosFavoritos(livro) {
    if (!favoritos.value.includes(livro)) {
      favoritos.value.push(livro);
    }
  }

  function livroNoCarrinho(livro) {
    return carrinho.value.includes(livro);
  }

  function livroNosFavoritos(livro) {
    return favoritos.value.includes(livro);
  }




  const livros = ref([
    { titulo: 'Conectadas', genero: 'romance', preco: 39.90 },
    { titulo: 'Canção dos Ossos', genero: 'romance', preco: 42.50 },
    { titulo: 'Algumas garotas são assim', genero: 'romance', preco: 35.00 },
    { titulo: 'Sua Alteza Real', genero: 'romance', preco: 45.90 },
    { titulo: 'Lembre-se de Nós', genero: 'romance', preco: 37.80 },
    { titulo: 'Os Sete Maridos de Evelyn Hugo', genero: 'romance', preco: 49.90 },
    { titulo: 'A Noite Passada no Telegraph Club', genero: 'romance', preco: 43.00 },
    { titulo: 'Luzes do Norte', genero: 'romance', preco: 38.50 },
    { titulo: 'Sombras do Sul', genero: 'romance', preco: 38.50 },
    { titulo: 'Fogo & Estrelas', genero: 'romance', preco: 41.90 },
    { titulo: 'Gelo & Sombras', genero: 'romance', preco: 41.90 },
    { titulo: 'Box O Senhor dos Anéis', genero: 'fantasia', preco: 149.90 },
    { titulo: 'As Crônicas de Nárnia', genero: 'fantasia', preco: 89.90 },
    { titulo: 'Box Harry Potter', genero: 'fantasia', preco: 189.90 },
    { titulo: 'Cidade dos Ossos', genero: 'fantasia', preco: 39.90 },
    { titulo: 'O Nome do Vento', genero: 'fantasia', preco: 54.90 },
    { titulo: 'Eragon', genero: 'fantasia', preco: 49.90 },
    { titulo: 'A Canção do Sangue', genero: 'fantasia', preco: 44.90 },
    { titulo: 'Ciclo da Herança', genero: 'fantasia', preco: 139.90 },
    { titulo: '1984', genero: 'ficcao', preco: 29.90 },
    { titulo: 'Eu, Robô', genero: 'ficcao', preco: 34.90 },
    { titulo: 'Box Duna', genero: 'ficcao', preco: 219.90 },
    { titulo: 'A Guerra dos Mundos', genero: 'ficcao', preco: 28.90 },
    { titulo: 'Contato', genero: 'ficcao', preco: 33.50 },
    { titulo: 'Perdido em Marte', genero: 'ficcao', preco: 41.90 },
    { titulo: 'Estação 11', genero: 'ficcao', preco: 36.00 },
    { titulo: 'Box Jurassic Park', genero: 'ficcao', preco: 79.90 },
    { titulo: 'Divergente', genero: 'distopia', preco: 34.90 },
    { titulo: 'Jogos Vorazes', genero: 'distopia', preco: 38.50 },
    { titulo: 'Maze Runner', genero: 'distopia', preco: 39.90 },
    { titulo: 'Vox', genero: 'distopia', preco: 41.50 },
    { titulo: 'O Homem do Castelo Alto', genero: 'distopia', preco: 36.90 },
    { titulo: 'O Último Homem', genero: 'distopia', preco: 35.90 },
    { titulo: 'A Estrada', genero: 'distopia', preco: 32.50 },
    { titulo: 'Revolução dos Bichos', genero: 'distopia', preco: 25.90 },
    { titulo: 'It: A Coisa', genero: 'terror', preco: 64.90 },
    { titulo: 'O Iluminado', genero: 'terror', preco: 59.90 },
    { titulo: 'Carrie, A Estranha', genero: 'terror', preco: 44.90 },
    { titulo: 'O Exorcista', genero: 'terror', preco: 49.90 },
    { titulo: 'O Silêncio dos Inocentes', genero: 'terror', preco: 39.90 },
    { titulo: 'Coraline', genero: 'terror', preco: 29.90 },
    { titulo: 'O Grito', genero: 'terror', preco: 33.90 },
    { titulo: 'O Labirinto', genero: 'terror', preco: 35.90 },
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
        <a href="#" class="icon-btn" @click.prevent="irParaFavoritos"><span class="fa-solid fa-heart"></span></a>
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

    <div v-else-if="paginaAtual === 'favoritos'" class="pagina-favoritos">
      <h2>Favoritos</h2>
      <p>Aqui vão aparecer seus livros favoritos futuramente!</p>
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

    <div class="bts">
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
      class="livro">
      <img :src="livro.imagem || '@/assets/placeholder.png'" :alt="livro.titulo" class="capa" />
      <p class="titulo">{{ livro.titulo }}</p>
      <p class="genero">({{ livro.genero }})</p>
      <p class="preco">
        <span v-if="inscrito">
          <s>R$ {{ livro.preco.toFixed(2) }}</s> <strong>R$ {{ (livro.preco * 0.9).toFixed(2) }}</strong>
        </span>
        <span v-else>
          <strong>R$ {{ livro.preco.toFixed(2) }}</strong>
        </span>
      </p>

    <div class="botoes">
      <button @click="adicionarAoCarrinho(livro)" :disabled="livroNoCarrinho(livro)">
        {{ livroNoCarrinho(livro) ? "Adicionado ✅" : "Adicionar ao Carrinho 🛒" }}
      </button>

      <button class="favoritar" @click="adicionarAosFavoritos(livro)">
        <span :class="['fa-heart', livroNosFavoritos(livro) ? 'favoritado' : '']"></span>
      </button>
    </div>
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
    <template v-if="!inscrito">
      <input
        type="email"
        placeholder="Insira seu email"
        v-model="emailUsuario"/>
      <button @click="inscreverEmail">Inscreva-se</button>
    </template>
    <template v-else>
      <p class="confirmacao">🎉 Parabéns! Você ganhou 10% de desconto!</p>
    </template>
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




