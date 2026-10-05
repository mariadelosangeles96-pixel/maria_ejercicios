<script setup>
import { ref } from 'vue'

const props = defineProps({
    camiseta: {
        type: Object,
        default : null
    }
});
const emits = defineEmits(['cerrar']);

const tallaSeleccionada = ref("S");
const precioFinalCamiseta = ref(0);

function actualizarPrecioFinalCamiseta() {
    let precioBase = camisetaSeleccionada.value.precio;
    if (tallaSeleccionada.value === "L") {
        precioBase += 2;
    }
    if (tallaSeleccionada.value === "XL") {
        precioBase += 3;
    }

    precioFinalCamiseta.value = precioBase;
}

</script>

<template>
    <div v-if="camiseta" class="modal" @click.self="$emit('cerrar')">
        <div class="contenido-modal">
            <h2 class="titulo-modal">{{ camiseta.nombre }}</h2>

            <div class="imagenes">
                <img :src="camiseta.imgFrente" alt="Por delante" />
                <img :src="camiseta.imgDetras" alt="Por detrás" />
            </div>

            <label for="select-talla">Elige tu talla: </label>
            <select v-model="tallaSeleccionada" @change="actualizarPrecioFinalCamiseta" name="seleccionar-talla"
                id="select-talla">
                <option value="S">S</option>
                <option value="M">M</option>
                <option value="L">L (+2€)</option>
                <option value="XL">XL (+3€)</option>
            </select>

            <p>Precio final: {{ precioFinalCamiseta }}€</p>

            <button @click="anadirAlCarrito" class="botones">Comprar</button>
            <button @click="$emit('cerrar')" class="botones">Cerrar</button>
        </div>
    </div>
</template>

<style scope>
.titulo-modal{
    color: #694F5D;
}

#select-talla{
    cursor: pointer;
}

.botones {
    margin: 1em;
    background-color: #68A691;
    color: white;
    border-radius: 0.3em;
    cursor: pointer;
}

.botones:hover {
    background-color: #EFC7C2;
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
    background-color: #FFE5D4;
    padding: 2em;
    border-radius: 1em;
    text-align: center;
    box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2);
    width: 90%;
    max-width: 600px;
    max-height: 80vh;
    overflow-y: auto;
    color: #694F5D;
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
    border: 1px solid #694F5D;
}
</style>