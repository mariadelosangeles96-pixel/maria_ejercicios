<script setup>
import { ref } from 'vue'
import Detalle from './Detalle.vue'
import camiseta1_front from '../assets/camiseta1_front.jpg'
import camiseta1_back from '../assets/camiseta1_back.jpg'

const precioFinalTotal = ref(0); //ESTE ES EL REACTIVO

const camisetas = [
    { id: 1, nombre: "Totoro", precio: 15, imgFrente: camiseta1_front, imgDetras: camiseta1_back },
    { id: 2, nombre: "Mononoke", precio: 25, imgFrente: camiseta1_front, imgDetras: camiseta1_back },
    { id: 3, nombre: "Chihiro", precio: 25, imgFrente: camiseta1_front, imgDetras: camiseta1_back },
    { id: 4, nombre: "Kiki", precio: 20, imgFrente: camiseta1_front, imgDetras: camiseta1_back },
    { id: 5, nombre: "Howl", precio: 20, imgFrente: camiseta1_front, imgDetras: camiseta1_back },
    { id: 6, nombre: "Arrietty", precio: 15, imgFrente: camiseta1_front, imgDetras: camiseta1_back },
];

const mostrarDetalle = ref(false);
</script>

<template>
    <div class="grid-camisetas">
        <article v-for="camiseta in camisetas" :key="camiseta.id" class="tarjeta" @click="mostrarDetalle = true">
            <img :src="camiseta.imgFrente" alt="Camiseta por delante" id="camiseta-catalogo">
            <br>
            <strong>{{ camiseta.nombre }} - {{ camiseta.precio }}€</strong>
            <p>Haz clic para ver detalles</p>
        </article>
    </div>

    <p> Precio final total: {{ precioFinalTotal }} </p>
</template>

<style scope>
body{
    background-color:rgb(175, 186, 240);
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
    width: 35%;
    border-radius: 1em;
    background-color: rgb(210, 238, 252);
    margin: 1em;
    padding: 0.5em;
    border: 1px solid rgb(61, 61, 68);
    cursor: pointer;
}

.botones {
    margin: 1em;
    background-color: rgb(140, 127, 146);
    color: aliceblue;
    border-radius: 0.3em;
}

.modal {
    position: fixed;
    top: 0;
    left: 0;
    width: 100vw;
    height: 100vh;
    background-color: rgba(0, 0, 0, 0.5);

    display: flex;
    justify-content: center;
    align-items: center;

    z-index: 1000;
}

.contenido-modal{
    background-color: white;
    padding: 2em;
    border-radius: 1em;
    text-align: center;
    box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2);

    width: 90%;
    max-width: 600px;
    max-height: 80vh;
    overflow-y: auto;
}

.imagenes{
    display: flex;
    justify-content: center;
    gap: 1em;
    margin: 1em 0;
}

.imagenes img {
    max-width: 45%;
    max-height: 300px;
    width: auto;
    height: auto;
    object-fit: contain;
    border-radius: 0.5em;
}
</style>