<script setup>
import { ref } from 'vue'
import Detalle from './Detalle.vue'
import camiseta1_front from '../assets/camiseta1_front.jpg'
import camiseta1_back from '../assets/camiseta1_back.jpg'

const emit = defineEmits(['anadir-al-carrito']);

const camisetas = ref([
    { id: 1, nombre: "Totoro", precio: 15, imgFrente: camiseta1_front, imgDetras: camiseta1_back, stock: { S: 5, M: 4, L: 2, XL: 1} },
    { id: 2, nombre: "Mononoke", precio: 25, imgFrente: camiseta1_front, imgDetras: camiseta1_back, stock: { S: 3, M: 5, L: 0, XL: 2 } },
    { id: 3, nombre: "Chihiro", precio: 25, imgFrente: camiseta1_front, imgDetras: camiseta1_back, stock: { S: 2, M: 2, L: 3, XL: 1 } },
    { id: 4, nombre: "Kiki", precio: 20, imgFrente: camiseta1_front, imgDetras: camiseta1_back, stock: { S: 4, M: 1, L: 5, XL: 0 } },
    { id: 5, nombre: "Howl", precio: 20, imgFrente: camiseta1_front, imgDetras: camiseta1_back, stock: { S: 1, M: 3, L: 2, XL: 4 } },
    { id: 6, nombre: "Arrietty", precio: 15, imgFrente: camiseta1_front, imgDetras: camiseta1_back, stock: { S: 5, M: 4, L: 1, XL: 1 } },
]);

const camisetaSeleccionada = ref(null);

function gestionarAnadirAlCarrito(producto){
    for (let i = 0; i < camisetas.value.length; i++) {
        if(camisetas.value[i].id === producto.id){
            if(camisetas.value[i].stock[producto.talla] > 0){
                camisetas.value[i].stock[producto.talla]--;
            };
        };
    };
    emit('anadir-al-carrito', producto);
};
</script>

<template>
    <div class="grid-camisetas">
        <article v-for="camiseta in camisetas" :key="camiseta.id" class="tarjeta" @click="camisetaSeleccionada = camiseta">
            <img :src="camiseta.imgFrente" alt="Camiseta por delante" id="camiseta-catalogo">
            <br>
            <strong>{{ camiseta.nombre }} - {{ camiseta.precio }}€</strong>
            <p>Haz clic para ver detalles</p>
        </article>
    </div>

    <Detalle :camiseta = "camisetaSeleccionada" @cerrar="camisetaSeleccionada = null" @anadir-al-carrito="gestionarAnadirAlCarrito" />

</template>

<style scope>
body{
    background-color: #FFE5D4;
}
.grid-camisetas {
    clear: both;
    padding: 2em;
    display: flex;
    justify-content: center;
    flex-wrap: wrap;
}

#camiseta-catalogo{
    max-width: 45%;
    max-height: 300px;
    width: auto;
    height: auto;
    border-radius: 0.5em;
}

article {
    width: 25%;
    border-radius: 1em;
    background-color: #EFC7C2;
    margin: 1em;
    padding: 0.5em;
    border: 1px solid #694F5D;
    cursor: pointer;
}
</style>