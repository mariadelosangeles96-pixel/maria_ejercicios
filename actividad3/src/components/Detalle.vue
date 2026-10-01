<script setup>
import { ref } from 'vue'
import camiseta1_front from '../assets/camiseta1_front.jpg'
import camiseta1_back from '../assets/camiseta1_back.jpg'

defineProps({
    visible: {
        type: Boolean,
        default: false
    }
})
defineEmits(['cerrar'])

const camisetaSeleccionada = ref(null);

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
    <div v-if="camisetaSeleccionada" class="modal" @click.self="camisetaSeleccionada = null">
        <div class="contenido-modal">
            <h2>{{ camisetaSeleccionada.nombre }}</h2>

            <div class="imagenes">
                <img :src="camisetaSeleccionada.imgFrente" alt="Por delante" />
                <img :src="camisetaSeleccionada.imgDetras" alt="Por detrás" />
            </div>

            <label for="select-talla">Elige tu talla:</label>
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