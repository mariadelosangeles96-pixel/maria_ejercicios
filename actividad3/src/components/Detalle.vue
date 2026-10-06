<script setup>
import { ref } from 'vue'

const props = defineProps({
    camiseta: {
        type: Object,
        default: null
    }
});
const emits = defineEmits(['cerrar', 'anadir-al-carrito']);

const tallaSeleccionada = ref("S");

function actualizarPrecioFinalCamiseta() {
    let precioBase = props.camiseta.precio;
    if (tallaSeleccionada.value === "L") {
        precioBase += 2;
    }
    if (tallaSeleccionada.value === "XL") {
        precioBase += 3;
    }

    return precioBase;
};

function anadirAlCarrito() {
    const stockDisponible = props.camiseta.stock[tallaSeleccionada.value];
    if (stockDisponible <= 0) {
        alert("No nos queda stock disponible en esta talla.");
        return;
    };

    emits('anadir-al-carrito', {
        id: props.camiseta.id,
        nombre: props.camiseta.nombre,
        talla: tallaSeleccionada.value,
        precioUnidad: actualizarPrecioFinalCamiseta(),
        imgFrente: props.camiseta.imgFrente
    });

    emit('cerrar');
};

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
            <select v-model="tallaSeleccionada" id="select-talla">
                <option value="S">S (Stock: {{ camiseta.stock.S }})</option>
                <option value="M">M (Stock: {{ camiseta.stock.M }})</option>
                <option value="L">L (+2€) (Stock: {{ camiseta.stock.L }})</option>
                <option value="XL">XL (+3€) (Stock: {{ camiseta.stock.XL }})</option>
            </select>

            <p>Precio final: {{ actualizarPrecioFinalCamiseta() }}€</p>

            <button @click="anadirAlCarrito" class="botones">Comprar</button>
            <button @click="$emit('cerrar')" class="botones">Cerrar</button>
        </div>
    </div>
</template>

<style scope>
.titulo-modal {
    color: #694F5D;
}

#select-talla {
    cursor: pointer;
    padding: 4px;
}

.botones {
    margin: 1em;
    padding: 8px 16px;
    background-color: #68A691;
    color: white;
    border: none;
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

.contenido-modal {
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

.imagenes {
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