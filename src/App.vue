<script setup>

import { ref, computed } from 'vue';

const valor = ref([]);


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


};
const name = "Bienvenido";


const mostrarmanito = computed(() => {

  if (valor.value != 0) {
    return true;
    
  } else {
    return false;
  }
  

});





</script>

<template>

  <div class="container-fluid">
    <div class="main">
      <h1 style="margin-top:60px">Hola {{ name }}</h1>

      <div class="moneda">
        <img width="150" height="150" v-for="(item, index) in coins" :key="index" :src="obtener_imagen(item.valor)"
          :id="'nueva_' + item.valor + '_pesos'" :title="item.valor + ' pesos'" @click="Guardar_mondeda(item.valor)" />
      </div>

      <div class="alcancia">
        <div v-show="mostrarmanit">
          <img src="./assets/manito.png" width="450" height="450" id="manito" />
        </div>
      </div>
    </div>
  </div>

</template>
<style scoped>
.alcancia {
  margin-top: 8.95em;
  height: 25em;
  background-repeat: no-repeat;
  background-position-x: center;
  background-size: 400px;
  background-image: url('./src/assets/cerdito.png')
}

#manito {
  cursor: pointer;
  transform: translate(40px,-150px);

}
</style>

