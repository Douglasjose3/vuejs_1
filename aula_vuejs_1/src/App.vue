<script setup>
import { reactive } from 'vue';

 // javascript
const nome = 'Douglas Rodrigues José'
const meuObj = {
  nome: 'Douglas',
  filmeFavorito: 'Resgate do soldado Ryan'
}

function dizOi (nome) {
  return `${nome} diz oi!`;
}

const enderecoDaImagemDoBatman = "https://media.newyorker.com/photos/6220ea493fb3bda1eed3aa3e/master/w_960,c_limit/220314_r40011.jpg";
const enderecoDaImagemDoSumperman = "https://cdn.media.amplience.net/s/hobbylobby/6006779-81166685-01082024-IMGSET?fmt=webp&w=544&h=544&sm=mc";
const gostaDoBatman = false;
const gostaDoSuperman = false;

const botaoDesabilitado = true;

const estaAutorizado = true;

// ESTADO da função
const estado = reactive({ //estado importa o reactive lá em cima do código e recebe um objeto
  contador: 0,
  email: '',
})
function incrementar() {
  estado.contador++;
}
function decrementar() {
  estado.contador--;
}

function alteraEmail(evento) {
  estado.email = evento.target.value;
}

//ESTILIZAÇÃO CONDICIONAL
const estadoTransferencia = reactive({
  saldo: 5000,
  transferindo: 0,
})

function mostrarSaldoFuturo() {
  const {saldo, transferindo} = estadoTransferencia;
  return saldo - transferindo;
}
function validaValorTransferencia() {
  const {saldo, transferindo} = estadoTransferencia;
  return saldo >= transferindo;
}

//LISTAS
const estadoNomesNaLista = reactive ({
  nomes: ['Douglas', 'Murilo', 'Vanessa', 'Julia'],
  nomesAInserir: '',
})
function cadastraNome() {
  if (estadoNomesNaLista.nomesAInserir.length >= 3) {
    estadoNomesNaLista.nomes.push(estadoNomesNaLista.nomesAInserir);
  } else {
    alert("Digite mais caracteres.");
  }
  console.log(estadoNomesNaLista);
}


</script>


<template> <!-- html -->

  <h1>{{ nome }}</h1> <!-- esse é modo de chamar o {{ script }} dentro do html -->
  <h2>{{ 10 + 10 }}</h2>
  <h3>{{ meuObj }}</h3>
  <h4>{{ dizOi('Murilo') }}</h4>
  <img v-bind:src="enderecoDaImagemDoBatman" alt=""> <!-- v-bind para ligar o script na tag. Podemos usar o v-bind ou só os :-->
  <img v-if="gostaDoBatman" :src="enderecoDaImagemDoBatman" alt=""> <!-- diretiva v-if="". v-if não aparece no DOM. v-show aparece do DOM quando inspecionamos o código -->
  <img v-else-if="gostaDoSuperman" :src="enderecoDaImagemDoSumperman" alt="">
  <h2 v-else>Não gosto de super herois</h2>
  <button :disabled="!botaoDesabilitado">Enviar mensagem</button> <!-- para negar uma constante usamos a ! -->
  <h2 v-if="estaAutorizado">Você está autorizado</h2>
  <h2 v-else>Não tem autorização</h2>

  <hr>

  {{ estado.contador }}
  <button @click="incrementar" type="button">+</button> <!-- para acessar ao eventor utilizar o @ -->
  <button @click="decrementar" type="button">-</button>

  <br>
  <hr>

  {{ estado.email }}
  <input type="email" @keyup="alteraEmail"> <!-- feedback instantâneo -->
  <br>
  <br>
  <input type="email" @change="alteraEmail"> <!-- change precisa sair do campo para mostrar o feedback -->

<br>
<hr>

Saldo: {{ estadoTransferencia.saldo }} <br>
Transferindo: {{ estadoTransferencia.transferindo }} <br>
Saldo depois da transferência: {{ mostrarSaldoFuturo() }} <br> <!-- não esquecer do () para function -->
<input class="campo" :class="{ invalido: !validaValorTransferencia() }" @keyup="evento => estadoTransferencia.transferindo = evento.target.value" type="number" placeholder="Digite o valor para transferência">
<button v-if="validaValorTransferencia()">Transferir</button>
<span v-else>Saldo insuficiente</span>

<br>
<hr>

<ul>
  <li v-for="nome in estadoNomesNaLista.nomes"> <!-- para interar usei a palavra nome in nomes (nome do array) -->
    {{ nome }}
  </li> 
</ul>
<input class="campo" @keyup="evento => estadoNomesNaLista.nomesAInserir = evento.target.value" type="text" placeholder="Digite un novo nome">
<button @click="cadastraNome" type="button">Adicionar</button>

<h3 v-for="nome in estadoNomesNaLista.nomes">{{ nome }}</h3>

</template>

<style scoped> /* css */
img {
  max-width: 130px;
  display: block;
  margin-top: 10px;
  margin-bottom: 10px;
}

button {
  margin-top: 10px;
  margin-bottom: 10px;
}

.invalido {
  outline-color: red;
  border-color: red;
}

.campo {
  background-color: rgb(228, 228, 228);
  margin-right: 10px;
}

</style>
