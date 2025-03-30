<script setup>
import { ref, watch } from 'vue'
const num = ref('')
const num2 = ref('')
const operador = ref('')
const resultado = ref('')

function adicionarNumero(numero) {
  if (operador.value != '') {
    num2.value = numero;
  } else {
    num.value = numero;
  }
}
function adicionarOperador(op) {
  if (num.value != '') {
    operador.value = op;
  }
}
function calcular() {
  if (operador.value != '') {
    if (operador.value == '+') {
      resultado.value = "= " + parseInt(num.value) + parseInt(num2.value);
    } else if (operador.value == '-') {
      resultado.value = "= " + parseInt(num.value) - parseInt(num2.value);
    } else if (operador.value == 'x') {
      resultado.value = "= " + parseInt(num.value) * parseInt(num2.value);
    } else if (operador.value == '/') {
      resultado.value = "= " + parseInt(num.value) / parseInt(num2.value);
    } else if (operador.value == '%') {
      resultado.value = "= " + (parseInt(num.value) / 100) * parseInt(num2.value);
      }
  }
}
function limpar() {
  num.value = '';
  num2.value = '';
  operador.value = '';
  resultado.value = '';
  }
</script>

<template>
  <div id="calculadora">
    <p>{{ num }} {{ operador }} {{ num2 }} {{ resultado }}</p>
    <div class="teclado">
      <div class="divisao">
        <button @click="limpar">AC</button>
        <button @click="apagar">C</button>
        <button @click="adicionarOperador('%')">%</button>
        <button @click="adicionarOperador('/')">/</button>
      </div>
      <div class="divisao">
        <button @click="adicionarNumero(9)">9</button>
        <button @click="adicionarNumero(8)">8</button>
        <button @click="adicionarNumero(7)">7</button>
        <button @click="adicionarOperador('x')">x</button>
      </div>
      <div class="divisao">
        <button @click="adicionarNumero(6)">6</button>
        <button @click="adicionarNumero(5)">5</button>
        <button @click="adicionarNumero(4)">4</button>
        <button @click="adicionarOperador('-')">-</button>
      </div>
      <div class="divisao">
        <button @click="adicionarNumero(3)">3</button>
        <button @click="adicionarNumero(2)">2</button>
        <button @click="adicionarNumero(1)">1</button>
        <button @click="adicionarOperador('+')">+</button>
      </div>
      <div class="divisao">
        <button @click="adicionarVirgula">,</button>
        <button @click="adicionarNumero(0)">0</button>
        <button id="btn-igual" @click="calcular">=</button>
      </div>
    </div>
  </div>

</template>

<style scoped>
div#calculadora {
  width: 20%;
  background-color: rgb(75, 0, 113);
  padding: 5px;
  border-radius: 10px;
  box-shadow: 0px 0px 10px rgba(0, 0,
      0, 0.5);
  border: 3px black solid;
  margin: 20px auto;
  text-align: center;
}

p {
  height: 70px;
  font-size: 40px;
  color: black;
  background-color: white;
  margin: 0.5vw 0 0.5vw 0;
  border: 1px black solid;
}

div#teclado {
  display: flex;
  justify-content: center;
}

div.colunas {
  display: grid;
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
  width: 140px;
  border-radius: 60px;
}
</style>
