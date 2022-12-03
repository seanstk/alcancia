

<script setup>
import { ref } from 'vue';
const coins = [
    { valor: 50 },
    { valor: 100 },
    { valor: 200 },
    { valor: 500 },
    { valor: 1000 },
];

const monedas=ref([]);
const cuantasmonedas=ref(0);
const totalmonedas=ref(0);
const monedastotales=ref(0);
const totalgeneral=ref(0);
const obtener_imagen = (e) => {
    var imagen = './src/assets/nueva_' + e + '.png';
    return imagen;

};


const consultar_Monedas = ((e)=>{
    
    monedas.value=JSON.parse(localStorage.getItem("valor"));
    // console.log(monedas);
    const coindb=Object.values((monedas.value ||[])).filter(coin=>coin===e)
    // console.log(coindb);
    
    cuantasmonedas.value=coindb.length
    totalmonedas.value=coindb.reduce((acc,el)=>{
        return acc+el
    },0)

    let total=Object.values((monedas.value||[]))
    monedastotales.value=total.length;
    totalgeneral.value=total.reduce((acc,el)=>(acc+el),0)

});

</script>
<template>
    <div class="modal" id="modal_alcancia" data-bs-backdrop="static" data-bs-keyboard="false" tabindex="-1"
        aria-labelledby="staticBackdropLabel" aria-hidden="true">
        <div class="modal-dialog">
            <div class="modal-content">
                <div class="modal-header">
                    <h5 class="modal-title" id="titulo">Consultar Alcancia</h5>
                    <button type="button" class="btn-close" data-bs-dismiss="modal" aria-label="Close"></button>
                </div>
                <div class="modal-body">
                    <div class="row">
                        <div class="col-md-12">
                            <div class="form-group">
                                <div class="moneda">
                                    <img width="80" height="80" v-for="(item, index) in coins" :key="index"
                                        :src="obtener_imagen(item.valor)" :id="'nueva_' + item.valor + '_pesos'"
                                        :title="item.valor + ' pesos'" @click="consultar_Monedas(item.valor)" />
                                </div>
                            </div>
                        </div>

                        <div class="col-md-12">
                            <div class="form-group">
                               cuantas monedas : {{cuantasmonedas}}
                                total monedas : {{totalmonedas}}
                            </div>
                        </div>
                        <div class="col-md-12">
                            <div class="form-group">
                               monedas totales : {{monedastotales}}
                                total monedas General: {{totalgeneral}}
                            </div>
                        </div>

                        


                    </div>
                </div>
                <div class="modal-footer">
                    <!-- <button type="button" class="btn btn-secondary" data-bs-dismiss="modal">Close</button>
                    <button type="button" class="btn btn-primary">Save changes</button> -->
                </div>
            </div>
        </div>
    </div>



</template>

<style scoped>

</style>