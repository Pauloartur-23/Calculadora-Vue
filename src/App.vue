<script setup>
import { ref, watch } from 'vue'
const tela = ref(0)
const numUm = ref(0)
const numDois = ref(0)
const resultado = ref()
const operacao = ref()

function add_sinal(sinal) {
  if (tela.value < 10) {
    if (sinal == 10) {
      tela.value = "+"
      operacao.value = "+"
    } else if (sinal == 11) {
      tela.value = "-"
      operacao.value = "-"
    } else if (sinal == 12) {
      tela.value = "X"
      operacao.value = "X"
    } else if (sinal == 13) {
      tela.value = "/"
      operacao.value = "/"
    }
  }
}
function add_numUm(numero) {
  if (numUm.value === 0) {
    numUm.value = numero;
    tela.value = numero;
  } else {
    numDois.value = numero;
    tela.value = numero;
  }
}
function calcular() {
  if (numUm.value === 0) {
    numUm.value = tela.value;
  } else {
    numDois.value = tela.value;
  }
  if (operacao.value == "+") {
    resultado.value = numUm.value + numDois.value;
    tela.value = resultado.value;
  } else if (operacao.value == "-") {
    resultado.value = numUm.value - numDois.value;
    tela.value = resultado.value;
  } else if (operacao.value == "X") {
    resultado.value = numUm.value * numDois.value;
    tela.value = resultado.value;
  } else if (operacao.value == "/") {
    resultado.value = numUm.value / numDois.value;
    tela.value = resultado.value;
  }

}
function limpar() {
  tela.value = 0;
  numUm.value = 0;
  numDois.value = 0;
  resultado.value = 0;
  operacao.value = "";
}

</script>

<template>
  <div id="calculadora">
  <h1>Calculadora</h1>
    <p id="painel">{{ tela }}</p>
    <div id="teclado">
      <div class="colunas">
        <button id="btn-c" @click="limpar()">C</button>
        <button id="btn-1" @click="add_numUm(1)">1</button>
        <button id="btn-7" @click="add_numUm(7)">7</button>
        <button id="btn-4" @click="add_numUm(4)">4</button>
      </div>
      <div class="colunas">
        <button id="btn-soma" @click="add_sinal(10)">+</button>
        <button id="btn-2" @click="add_numUm(2)">2</button>
        <button id="btn-5" @click="add_numUm(5)">5</button>
        <button id="btn-8" @click="add_numUm(8)">8</button>
      </div>
      <div class="colunas">
        <button id="btn-subtracao" @click="add_sinal(11)">-</button>
        <button id="btn-3" @click="add_numUm(3)">3</button>
        <button id="btn-6" @click="add_numUm(6)">6</button>
        <button id="btn-9" @click="add_numUm(9)">9</button>
      </div>
      <div class="colunas">
        <button id="btn-multiplicacao" @click="add_sinal(12)">x</button>
        <button id="btn-divisao" @click="add_sinal(13)">/</button>
        <button id="btn-igual" @click="calcular()">=</button>
      </div>
      </div>
    </div>
</template>

<style scoped>
div#calculadora{
  width: 20%;
  background-color: rgb(75, 0, 113);
  padding: 10px;
  border-radius: 10px;
  box-shadow: 0px 0px 10px rgba(0, 0,
  0, 0.5);
  border: 3px black solid;
  margin: 20px auto;
  text-align: center;
}
p{
  font-size: 40px;
  color: black;
  background-color: white;
  margin: 0.5vw 0 0.5vw 0;
  border: 1px black solid;
}
div#teclado{
  display: flex;
  justify-content: center;
}
div.colunas{
  display:grid;
}
button {
  width: 70px;
  height: 70px;
  font-size: 30px;
  border: 1px black solid;
  border-radius: 100%;
  background-color: rgb(255, 255, 255);

}

button#btn-igual {
  height: 140px;
  border-radius: 60px;
  background-color: rgb(143, 0, 148);
  color: white;
}
</style>
