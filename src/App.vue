<script setup>
import { ref, computed, watch, nextTick, onMounted, onBeforeUnmount } from 'vue';

const tela = ref([]);
const telaview = computed(() => tela.value.join(""));

const painelRef = ref(null);

function addTela(item) {
  tela.value.push(item);
}

function clearTela() {
  tela.value = [];
}

function resultTela() {
  try {
    const resultado = new Function(`return ${telaview.value}`)();
    tela.value = [resultado];
  } catch (e) {
    tela.value = ['Erro'];
  }
}

watch(telaview, () => {
  nextTick(() => {
    if (painelRef.value) {
      painelRef.value.scrollLeft = painelRef.value.scrollWidth;
    }
  });
});

function handleWheelScroll(event) {
  if (painelRef.value) {
    event.preventDefault();
    painelRef.value.scrollLeft += event.deltaY;
  }
}

onMounted(() => {
  if (painelRef.value) {
    painelRef.value.addEventListener('wheel', handleWheelScroll, { passive: false });
  }
});

onBeforeUnmount(() => {
  if (painelRef.value) {
    painelRef.value.removeEventListener('wheel', handleWheelScroll);
  }
});
</script>

<template>
  <div id="calculadora">
    <h1>Calculadora</h1>
    <div id="painel" ref="painelRef">{{ telaview }}</div>
    <div id="teclado">
      <div class="linha">
        <button class="acao" @click="clearTela">C</button>
        <button @click="addTela(7)">7</button>
        <button @click="addTela(4)">4</button>
        <button @click="addTela(1)">1</button>
        <button @click="addTela('.')">.</button>
      </div>
      <div class="linha">
         <button @click="addTela('/')">÷</button>
        <button @click="addTela(8)">8</button>
        <button @click="addTela(5)">5</button>
        <button @click="addTela(2)">2</button>
        <button @click="addTela(0)">0</button>
      </div>
      <div class="linha">
        <button @click="addTela('*')">×</button>
        <button @click="addTela(9)">9</button>
        <button @click="addTela(6)">6</button>
        <button @click="addTela(3)">3</button>
        <button @click="addTela('.')">.</button>
      </div>
      <div class="linha">
        <button @click="addTela('-')">−</button>
        <button @click="addTela('+')">+</button>
        <button id="btn-igual" @click="resultTela">=</button>
      </div>
    </div>
  </div>
</template>

<style scoped>
* {
  font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
  box-sizing: border-box;
}

#calculadora {
  max-width: 400px;
  width: 90%;
  background-color: #009ab2;
  padding: 20px;
  border-radius: 16px;
  box-shadow: 0 10px 25px rgba(0, 0, 0, 0.15);
  margin: 40px auto;
  text-align: center;
  border: 2px solid #000000;
}

h1 {
  margin-bottom: 20px;
  font-size: 28px;
  color: #000000;
}

#painel {
  font-size: 36px;
  color: #222;
  background-color: #ffffff;
  border: 2px solid #000000;
  border-radius: 8px;
  padding: 5px 10px 10px 10px;
  margin-bottom: 20px;
  height: 60px;
  overflow-x: auto;
  white-space: nowrap;
  text-align: right;
  scroll-behavior: smooth;
  scrollbar-width: none;
  -ms-overflow-style: none;
}
#painel::-webkit-scrollbar {
  display: none;
}

#teclado {
  display: flex;
  gap: 10px;
}

.linha {
  display: grid;
  gap: 10px;
  flex-wrap: wrap;
}

button {
  flex: 1 1 60px;
  width: 80px;
  height: 80px;
  font-size: 24px;
  border: 1px black solid;
  border-radius: 12px;
  background-color: #c9fffc;
  box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
  transition: all 0.2s ease;
  color: #000000;
}

button:hover {
  background-color: #9afffa;
  transform: translateY(-2px);
}

button:active {
  transform: scale(0.98);
  box-shadow: inset 0 2px 4px rgba(0, 0, 0, 0.2);
}

button.acao {
  background-color: #004158;
  color: white;
}

button.acao:hover {
  background-color: #002e3f;
}

#btn-igual {
  background-color: #004158;
  color: white;
  height: 240px;
}

#btn-igual:hover {
  background-color: #002e3f;
}
</style>
