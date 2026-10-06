<script setup>
import { ref } from 'vue'
import Cabecera from './components/Cabecera.vue'
import Cuerpo from './components/Cuerpo.vue'
import Carrito from './components/Carrito.vue'
import Pie from './components/Pie.vue'

const carrito = ref([])
const mostrarCarrito = ref(false)

function agregarAlCarrito(producto) {
  carrito.value.push(producto)
}

function eliminarDelCarrito(indice) {
  carrito.value.splice(indice, 1)
}
</script>

<template>
  <div id="app-container">
    <Cabecera 
      :cantidad-carrito="carrito.length" 
      @abrir-carrito="mostrarCarrito = !mostrarCarrito" 
    />

    <Cuerpo @anadir-al-carrito="agregarAlCarrito" />

    <Carrito 
      v-if="mostrarCarrito" 
      :carrito="carrito" 
      @eliminar-item="eliminarDelCarrito" 
      @cerrar="mostrarCarrito = false" 
    />

    <Pie />
  </div>
</template>

<style>
body {
  background-color: #FFE5D4;
  margin: 0;
  font-family: Arial, Helvetica, sans-serif;
}
</style>