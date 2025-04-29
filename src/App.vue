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
  const item = carrinho.value.find(item => item.livro.id === livro.id);
    if (item) {
      item.quantidade++;
    } else {
     carrinho.value.push({ livro, quantidade: 1 });
    }
  }

  function removerDoCarrinho(livro) {
    carrinho.value = carrinho.value.filter(item => item.livro.id !== livro.id);
  }

  function aumentarQuantidade(livro) {
  const item = carrinho.value.find(item => item.livro.id === livro.id);
    if (item) item.quantidade++;
  }

  function diminuirQuantidade(livro) {
  const item = carrinho.value.find(item =>  item.livro.id === livro.id);
    if (item && item.quantidade > 1) {
      item.quantidade--;
    } else {
    removerDoCarrinho(livro);
    }
  }
  const totalCarrinho = computed(() =>
    carrinho.value.reduce((total, item) => total + item.livro.preco * item.quantidade, 0)
  );


  function livroNoCarrinho(livro) {
    return carrinho.value.includes(livro);
  }

  function livroNosFavoritos(livro) {
    return favoritos.value.includes(livro);
  }

  function adicionarAosFavoritos(livro) {
  const item = favoritos.value.find(item => item.livro.id === livro.id);
    if (item) {
      item.quantidade++;
    } else {
     favoritos.value.push({ livro, quantidade: 1 });
    }
  }

  const totalFavoritos = computed(() =>
    favoritos.value.reduce((total, item) => total + item.livro.preco * item.quantidade, 0)
  );

  function removerFavoritos(livro) {
    favoritos.value = favoritos.value.filter(item => item.livro.id !== livro.id);
  }
  


  const livros = ref([

    { id: '101', titulo: 'Conectadas', autor: 'Clara Alves', genero: 'romance', preco: 25.27, imagem: new URL('@/assets/images/conectadas.jpg', import.meta.url).href},
    { id: '102', titulo: 'Canção dos Ossos', autor: 'Giu Domingues',genero: 'romance', preco: 36.30, imagem: new URL('@/assets/images/cancao_dos_ossos.jpg', import.meta.url).href },
    { id: '103', titulo: 'Algumas garotas são assim', autor: 'Jennifer Dugan', genero: 'romance', preco: 36.24, imagem: new URL('@/assets/images/algumas_garotas_sao_assim.jpg', import.meta.url).href },
    { id: '104', titulo: 'Sua Alteza Real', autor: 'Rachel Hawkins', genero: 'romance', preco: 33.73, imagem: new URL('@/assets/images/sua_alteza_real.jpg', import.meta.url).href },
    { id: '105', titulo: 'Lembre-se de Nós', autor: 'Alyson Derrick', genero: 'romance', preco: 43.92, imagem: new URL('@/assets/images/lembre-se_de_nos.jpg', import.meta.url).href },
    { id: '106', titulo: 'Os Sete Maridos de Evelyn Hugo',autor: 'Taylor Jenkins Reid', genero: 'romance', preco: 48.90, imagem: new URL('@/assets/images/os_sete_maridos_de_evelyn_hugo.jpg', import.meta.url).href },
    { id: '107', titulo: 'A Noite Passada no Telegraph Club', autor: 'Melinda Lo',genero: 'romance', preco: 41.90, imagem: new URL('@/assets/images/a_noite_passada_no_telegraph_club.jpg', import.meta.url).href },
    { id: '108', titulo: 'Luzes do Norte', autor: 'Giu Domingues',genero: 'romance', preco: 44.17, imagem: new URL('@/assets/images/luzes_do_norte.jpg', import.meta.url).href },
    { id: '109', titulo: 'Sombras do Sul', autor: 'Giu Domingues',genero: 'romance', preco: 44.93, imagem: new URL('@/assets/images/sombras_do_sul.jpg', import.meta.url).href },
    { id: '110', titulo: 'Fogo & Estrelas', autor: 'Audrey Coulthurst',genero: 'romance', preco: 42.94, imagem: new URL('@/assets/images/fogo_e_estrelas.jpg', import.meta.url).href },
    { id: '111', titulo: 'Gelo & Sombras', autor: 'Audrey Coulthurst',genero: 'romance', preco: 54.96, imagem: new URL('@/assets/images/gelo_e_sombras.jpg', import.meta.url).href },
    { id: '112', titulo: 'Ultima parada', autor: 'Casey McQuiston',genero: 'romance', preco: 22.99, imagem: new URL('@/assets/images/ultima_parada.jpg', import.meta.url).href },
    { id: '113', titulo: 'Imogen, obviamente', autor: 'Becky Albertalli',genero: 'romance', preco: 37.10, imagem: new URL('@/assets/images/imogen_obviamente.jpg', import.meta.url).href },
    { id: '114', titulo: 'É assim que se perde a guerra do tempo', autor: ' Amal El-Mohtar e Max Gladstone',genero: 'romance', preco: 48.46, imagem: new URL('@/assets/images/e_assim_que_se_perde_a_guerra_do_tempo.jpg', import.meta.url).href },
    { id: '115', titulo: 'Cinderela está morta', autor: 'Kalynn Bayron',genero: 'romance', preco: 24.69, imagem: new URL('@/assets/images/cinderela_esta_morta.jpg', import.meta.url).href },


    { id: '201', titulo: 'As Crônicas de Nárnia', autor: 'C.S. Lewis',genero: 'fantasia', preco: 33.16, imagem: new URL('@/assets/images/as_cronicas_de_narnia.jpg', import.meta.url).href },
    { id: '202', titulo: 'O Nome do Vento', autor: 'Patrick Rothfuss',genero: 'fantasia', preco: 55.99, imagem: new URL('@/assets/images/o_nome_do_vento.jpg', import.meta.url).href },
    { id: '203', titulo: 'Ciclo A Herança', autor: 'Christopher Paolini',genero: 'fantasia', preco: 85.02, imagem: new URL('@/assets/images/ciclo_a_herança.jpg', import.meta.url).href },
    { id: '204', titulo: 'Nevernight: A Sombra do Corvo', autor: 'Jay Kristoff',genero: 'fantasia', preco: 67.16, imagem: new URL('@/assets/images/nevernight.jpeg', import.meta.url).href },
    { id: '205', titulo: 'Godsgrave: O Espetáculo Sangrento', autor: 'Jay Kristoff',genero: 'fantasia', preco: 71.87, imagem: new URL('@/assets/images/godsgrave.jpeg', import.meta.url).href },
    { id: '206', titulo: 'Darkdawn: As Cinzas da República', autor: 'Jay Kristoff',genero: 'fantasia', preco: 77.05, imagem: new URL('@/assets/images/darkdawn.jpeg', import.meta.url).href },
    { id: '207', titulo: 'A Quinta Estação', autor: 'N.K. Jemisin',genero: 'fantasia', preco: 52.50, imagem: new URL('@/assets/images/a_quinta_estacao.jpeg', import.meta.url).href },
    { id: '208', titulo: 'O Portão do Obelisco', autor: 'N.K. Jemisin',genero: 'fantasia', preco: 73.19, imagem: new URL('@/assets/images/o_portao_do_obelisco.jpeg', import.meta.url).href },
    { id: '209', titulo: 'O Céu de Pedra', autor: 'N.K. Jemisin',genero: 'fantasia', preco: 68.60, imagem: new URL('@/assets/images/o_ceu_de_pedra.jpeg', import.meta.url).href },
    { id: '210', titulo: 'Sombra e Ossos', autor: 'Leigh Bardugo',genero: 'fantasia', preco: 54.92, imagem: new URL('@/assets/images/sombra_e_ossos.jpeg', import.meta.url).href },
    { id: '211', titulo: 'Sol e Tormenta', autor: 'Leigh Bardugo',genero: 'fantasia', preco: 47.55, imagem: new URL('@/assets/images/sol_e_tormenta.jpeg', import.meta.url).href },
    { id: '212', titulo: 'Ruína em Ascensão', autor: 'Leigh Bardugo',genero: 'fantasia', preco: 54.57, imagem: new URL('@/assets/images/ruina_em_ascensao.jpeg', import.meta.url).href },
    { id: '213', titulo: 'Mistborn: O Império Final', autor: 'Branden Sanderson',genero: 'fantasia', preco: 70.02, imagem: new URL('@/assets/images/mistborn_o_imperio_final.jpeg', import.meta.url).href },
    { id: '214', titulo: 'Mistborn: O Poço da Ascensão', autor: 'Branden Sanderson',genero: 'fantasia', preco: 71.22, imagem: new URL('@/assets/images/mistborn_poco_da_ascensao.jpeg', import.meta.url).href },
    { id: '215', titulo: 'Mistborn: O Herói das Eras', autor: 'Branden Sanderson',genero: 'fantasia', preco: 75.96, imagem: new URL('@/assets/images/mistborn_o_heroi_das_eras.jpeg', import.meta.url).href },


    { id: '301', titulo: '1984',autor: 'George Orwell', genero: 'ficcao', preco: 16.86, imagem: new URL('@/assets/images/1984.jpg', import.meta.url).href },
    { id: '302', titulo: 'Eu, Robô', autor: 'Isaac Asimov',genero: 'ficcao', preco: 23.47, imagem: new URL('@/assets/images/eu_robo.jpg', import.meta.url).href },
    { id: '303', titulo: 'A Guerra dos Mundos', autor: 'H.G. Wells',genero: 'ficcao', preco: 47.49, imagem: new URL('@/assets/images/a_guerra_dos_mundos.jpg', import.meta.url).href },
    { id: '304', titulo: 'Contato', autor: 'Carl Sagan',genero: 'ficcao', preco: 54.08, imagem: new URL('@/assets/images/contato.jpg', import.meta.url).href },
    { id: '305', titulo: 'Perdido em Marte', autor: 'Andy Weir',genero: 'ficcao', preco: 18.99, imagem: new URL('@/assets/images/perdido_em_marte.jpg', import.meta.url).href },
    { id: '306', titulo: 'Estação 11', autor: 'Emily St. John Mandel ',genero: 'ficcao', preco: 35.91, imagem: new URL('@/assets/images/estacao_11.jpg', import.meta.url).href },
    { id: '307', titulo: 'Fundação', autor: 'Isaac Asimov',genero: 'ficcao', preco: 49.08, imagem: new URL('@/assets/images/fundacao.jpg', import.meta.url).href },
    { id: '308', titulo: 'Fundação e Império', autor: 'Isaac Asimov',genero: 'ficcao', preco: 61.05, imagem: new URL('@/assets/images/fundacao_e_imperio.jpg', import.meta.url).href },
    { id: '309', titulo: 'Segunda Fundação', autor: 'Isaac Asimov',genero: 'ficcao', preco: 57.89, imagem: new URL('@/assets/images/segunda_fundacao.jpg', import.meta.url).href },
    { id: '310', titulo: 'Limites da Fundação', autor: 'Isaac Asimov',genero: 'ficcao', preco: 69.17, imagem: new URL('@/assets/images/limites_da_fundacao.jpg', import.meta.url).href },
    { id: '311', titulo: 'Fundação e Terra', autor: 'Isaac Asimov',genero: 'ficcao', preco: 55.22, imagem: new URL('@/assets/images/fundacao_e_terra.jpg', import.meta.url).href },
    { id: '312', titulo: 'Prelúdio à Fundação', autor: 'Isaac Asimov',genero: 'ficcao', preco: 61.01, imagem: new URL('@/assets/images/preludio_a_fundacao.jpg', import.meta.url).href },
    { id: '313', titulo: 'Origens da Fundação', autor: 'Isaac Asimov',genero: 'ficcao', preco: 99.99, imagem: new URL('@/assets/images/origens_da_fundacao.jpg', import.meta.url).href },
    { id: '314', titulo: 'Vilão', autor: 'V.E Schwab',genero: 'ficcao', preco: 42.78, imagem: new URL('@/assets/images/vilao.jpg', import.meta.url).href },
    { id: '315', titulo: 'Vingança', autor: 'V.E Schwab',genero: 'ficcao', preco: 47.94, imagem: new URL('@/assets/images/vinganca.jpg', import.meta.url).href },

    { id: '401', titulo: 'Vox', autor: 'Christina Dalcher',genero: 'distopia', preco: 19.90, imagem: new URL('@/assets/images/vox.jpg', import.meta.url).href },
    {  id: '402', titulo: 'O Homem do Castelo Alto', autor: 'Philip K. Dick',genero: 'distopia', preco: 42.87, imagem: new URL('@/assets/images/o_homem_do_castelo_alto.jpg', import.meta.url).href },
    { id: '403', titulo: 'O Último Homem', autor: 'Mary Shelley',genero: 'distopia', preco: 55.44, imagem: new URL('@/assets/images/o_ultimo_homem.jpg', import.meta.url).href },
    { id: '404', titulo: 'A Estrada', autor: 'Cormac McCarthy',genero: 'distopia', preco: 30.00, imagem: new URL('@/assets/images/a_estrada.jpg', import.meta.url).href },
    { id: '405', titulo: 'Revolução dos Bichos', autor: 'George Orwell',genero: 'distopia', preco: 16.78, imagem: new URL('@/assets/images/revolucao_dos_bichos.jpeg', import.meta.url).href },
    { id: '406', titulo: 'O Ceifador', autor: 'Neal Shusterman',genero: 'distopia', preco: 55.93, imagem: new URL('@/assets/images/o_ceifador.jpg', import.meta.url).href },
    { id: '407', titulo: 'A Nuvem', autor: 'Neal Shusterman',genero: 'distopia', preco: 62.83, imagem: new URL('@/assets/images/a_nuvem.jpg', import.meta.url).href },
    { id: '408', titulo: 'O Timbre', autor: 'Neal Shusterman',genero: 'distopia', preco: 51.96, imagem: new URL('@/assets/images/o_timbre.jpg', import.meta.url).href },
    { id: '409', titulo: 'O Conto da Aia', autor: 'Margaret Atwood',genero: 'distopia', preco: 20.99, imagem: new URL('@/assets/images/o_conto_da_aia.jpg', import.meta.url).href },
    { id: '410', titulo: 'Jogador Número Um', autor: 'Ernest Cline',genero: 'distopia', preco: 19.99, imagem: new URL('@/assets/images/jogador_numero_um.jpeg', import.meta.url).href },
    { id: '411', titulo: 'O Doador de Memórias', autor: 'Lois Lowry',genero: 'distopia', preco: 15.77, imagem: new URL('@/assets/images/o_doador_de_memorias.jpeg', import.meta.url).href },
    { id: '412', titulo: 'Estação Onze', autor: 'Emily St. John Mandel',genero: 'distopia', preco: 35.91, imagem: new URL('@/assets/images/estacao_11.jpg', import.meta.url).href },
    { id: '413', titulo: 'Silo', autor: 'Hugh Howey',genero: 'distopia', preco: 49.41, imagem: new URL('@/assets/images/silo.jpeg', import.meta.url).href },
    { id: '414', titulo: 'Ordem', autor: 'Hugh Howey',genero: 'distopia', preco: 23.94, imagem: new URL('@/assets/images/ordem.jpg', import.meta.url).href },
    { id: '415', titulo: 'Legado', autor: 'Hugh Howey',genero: 'distopia', preco: 29.94, imagem: new URL('@/assets/images/legado.jpg', import.meta.url).href },


    { id: '501', titulo: 'It: A Coisa', autor: 'Stephen king',genero: 'terror', preco: 106.20, imagem: new URL('@/assets/images/it_a_coisa.jpg', import.meta.url).href },
    { id: '502', titulo: 'O Iluminado', autor: 'Stephen King',genero: 'terror', preco: 59.30, imagem: new URL('@/assets/images/o_iluminado.jpg', import.meta.url).href },
    { id: '503', titulo: 'Carrie, A Estranha', autor: 'Stephen King',genero: 'terror', preco: 49.06, imagem: new URL('@/assets/images/carrie_a_estranha.jpg', import.meta.url).href },
    { id: '504', titulo: 'O Exorcista', autor: 'William Peter Blatty',genero: 'terror', preco: 38.49, imagem: new URL('@/assets/images/o_exorcista.jpg', import.meta.url).href },
    { id: '505', titulo: 'O Silêncio dos Inocentes', autor: 'Thomas Harris',genero: 'terror', preco: 58.28, imagem: new URL('@/assets/images/o_silencio_dos_inocentes.jpg', import.meta.url).href },
    { id: '506', titulo: 'Coraline', autor: 'Neil Gaiman',genero: 'terror', preco: 58.85, imagem: new URL('@/assets/images/coraline.jpg', import.meta.url).href },
    { id: '507', titulo: 'O Labirinto', autor: 'Kate Mosse',genero: 'terror', preco: 99.99, imagem: new URL('@/assets/images/o_labirinto.jpg', import.meta.url).href },
    { id: '508', titulo: 'Hell House: A Casa do Inferno', autor: 'Richard Matheson',genero: 'terror', preco: 57.17, imagem: new URL('@/assets/images/hell_house.jpg', import.meta.url).href },
    { id: '509', titulo: 'A Noite dos Mortos-Vivos', autor: ' John Russo',genero: 'terror', preco: 17.43, imagem: new URL('@/assets/images/a_noite_dos_mortos_vivos.jpg', import.meta.url).href },
    { id: '510', titulo: 'Gótico Mexicano', autor: 'Silvia Moreno-Garcia',genero: 'terror', preco: 45.94, imagem: new URL('@/assets/images/gotico_mexicano.jpg', import.meta.url).href },
    { id: '511', titulo: 'A Garota da Casa ao Lado', autor: 'Jack Ketchum',genero: 'terror', preco: 62.11, imagem: new URL('@/assets/images/a_garota_da_casa_ao_lado.jpg', import.meta.url).href },
    { id: '512', titulo: 'Os Condenados', autor: 'Andrew Pyper',genero: 'terror', preco: 67.61, imagem: new URL('@/assets/images/os_condenados.jpg', import.meta.url).href },
    { id: '513', titulo: 'Hex: Uma Bruxa Clássica', autor: 'Thomas Olde Heuvelt',genero: 'terror', preco: 57.32, imagem: new URL('@/assets/images/hex.jpg', import.meta.url).href },
    { id: '514', titulo: 'O Demonologista', autor: 'Andrew Pyper',genero: 'terror', preco: 38.45, imagem: new URL('@/assets/images/o_demonologista.jpg', import.meta.url).href },
    { id: '515', titulo: 'A Morte da Sra Westaway', autor: 'Ruth Ware',genero: 'terror', preco: 48.23, imagem: new URL('@/assets/images/a_morte_da_sra_westaway.jpg', import.meta.url).href },
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
  setInterval(proximoLivro, 10000)
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

      <div v-if="carrinho.length === 0">
        <p>Seu carrinho está vazio por enquanto.</p>
      </div>

      <div v-else>
        <ul>
          <li v-for="item in carrinho" :key="item.livro.id" class="item-carrinho">
            <img :src="item.livro.imagem" alt="Capa do livro" class="imagem-livro" />
            <div class="info-livro">
            <h3>{{ item.livro.titulo }}</h3>
            <p>Preço: R$ {{ item.livro.preco.toFixed(2) }}</p>
            </div>

            <div class="botoes-carrinho">
              <div class="quantidade-control">
              <button @click="aumentarQuantidade(item.livro)">+</button>
              <p>{{ item.quantidade }}</p>
              <button @click="diminuirQuantidade(item.livro)">-</button>
              </div>
              <button @click="removerDoCarrinho(item.livro)">REMOVER</button>
            </div>
          </li>
        </ul>
      </div>
      <div class="total-voltar">
        <h3>Total: R$ {{ totalCarrinho.toFixed(2) }}</h3>
        <button @click="irParaHome">Voltar</button>
      </div>
    </div>



    <div v-else-if="paginaAtual === 'favoritos'" class="pagina-favoritos">
      <h2>Favoritos</h2>

    <div v-if="favoritos.length === 0">  
      <p>Aqui vão aparecer seus livros favoritos futuramente!</p>
    </div>

    <div v-else>
      <ul>
        <li v-for="item in favoritos" :key="item.livro.id" class="item-favoritos">
          <img :src="item.livro.imagem" alt="Capa do livro" class="imagem-livro">
          <div class="if-livro">
            <h3>{{ item.livro.titulo }}</h3>
            <p>Preço: R$ {{ totalFavoritos.toFixed(2) }}</p>
          </div>

          <div class="bnts-fav">
            <button @click="removerFavoritos(item.livro)">REMOVER</button>
            <button @click="adicionarAoCarrinho(item.livro)">ADICIONAR AO CARRINHO</button>
          </div>
        </li>
      </ul>
    </div>
    <div class="ttl-volt">
      <div class="total-voltar">
        <h3>Total: R$ {{ totalFavoritos.toFixed(2) }}</h3>
        <button @click="irParaHome">Voltar</button>
    </div>
    </div>
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
    <div class="generos"  style="display: flex; gap: 20px; flex-wrap: wrap; justify-content: center; margin-top: 20px;">
      <button class="todos" @click="filtrar('todos')">Todos</button>
      <button class="fantasia" @click="filtrar('fantasia')">Fantasia</button>
      <button class="romance" @click="filtrar('romance')">Romance</button>
      <button class="distopia" @click="filtrar('distopia')">Distopia</button>
      <button class="ficcao" @click="filtrar('ficcao')">Ficção Científica</button>
      <button class="terror" @click="filtrar('terror')">Terror</button>
    </div>
    </div>

    <div class="livros">
    <div
      v-for="livro in livrosFiltrados"
      :key="livro.titulo"
      class="livro">
      <img :src="livro.imagem || '@/assets/placeholder.png'" :alt="livro.titulo" class="capa" />
      <p class="titulo">{{ livro.titulo }}</p>
      <p class="genero">{{ livro.autor }}</p>
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




