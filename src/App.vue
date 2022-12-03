<script setup>

import { ref, computed, watch } from 'vue';
import informacion from './components/informacion.vue';

const valor = ref([]);
const mostrarmanito = ref(false);


const coins = [
  { valor: 50 },
  { valor: 100 },
  { valor: 200 },
  { valor: 500 },
  { valor: 1000 },
];

const obtener_imagen = (e) => {
  var imagen = './src/assets/nueva_' + e + '.png';
  return imagen;

};

const Guardar_mondeda = (e) => {


  valor.value.push(e);
  localStorage.setItem('valor', JSON.stringify(valor.value));
  mostrarmanito.value = true;

};
const name = "Bienvenido";

watch(mostrarmanito, (value) => {
  if (value) {
    setTimeout(() => {
      mostrarmanito.value = false;
    }, 500);
  }
})



</script>

<template>
  <div class="container-fluid" id="homePage">
    <div class="main">
      <h1>Hola {{ name }}</h1>

      <div class="moneda">
        <img width="150" height="150" v-for="(item, index) in coins" :key="index" :src="obtener_imagen(item.valor)"
          :id="'nueva_' + item.valor + '_pesos'" :title="item.valor + ' pesos'" @click="Guardar_mondeda(item.valor)" />
      </div>

      <div>
        <div v-if="(mostrarmanito)">
          <img src="./assets/manito.png" width="350" height="350" id="manito" />
        </div>
      </div>

      <div class="pig-container">
        <img src="./assets/cerdito.png" alt="cerdito-img" height="300"  data-bs-toggle="modal" data-bs-target="#modal_alcancia">
      </div>
            
      <informacion></informacion>
    </div>
  </div>
</template>
<style scoped>
#homePage {
  min-height: 100vh;
  position: relative;
}

.pig-container {
  position: absolute;
  top: 65%;
  left: 50%;
  transform: translate(-50%, -50%);
  z-index: 1;

}

#manito {
  position: absolute;
  cursor: pointer;
  top: 45%;
  left: 52%;
  transform: translate(-50%, -50%);
  z-index: 2;
}
</style>

