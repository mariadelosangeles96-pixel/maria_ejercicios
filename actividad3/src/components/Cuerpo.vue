<script setup>
import { ref } from 'vue'
import Detalle from './Detalle.vue'
import camiseta1_front from '../assets/camiseta1_front.jpg'
import camiseta1_back from '../assets/camiseta1_back.jpg'

const precioFinalTotal = ref(0);

const camisetas = [
    { id: 1, nombre: "Totoro", precio: 15, imgFrente: camiseta1_front, imgDetras: camiseta1_back },
    { id: 2, nombre: "Mononoke", precio: 25, imgFrente: camiseta1_front, imgDetras: camiseta1_back },
    { id: 3, nombre: "Chihiro", precio: 25, imgFrente: camiseta1_front, imgDetras: camiseta1_back },
    { id: 4, nombre: "Kiki", precio: 20, imgFrente: camiseta1_front, imgDetras: camiseta1_back },
    { id: 5, nombre: "Howl", precio: 20, imgFrente: camiseta1_front, imgDetras: camiseta1_back },
    { id: 6, nombre: "Arrietty", precio: 15, imgFrente: camiseta1_front, imgDetras: camiseta1_back },
];

const camisetaSeleccionada = ref(null);
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

    <Detalle :camiseta = "camisetaSeleccionada" @cerrar="camisetaSeleccionada = null" />

    <p> Precio final total: {{ precioFinalTotal }} </p>
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