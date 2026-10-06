<script setup>
const props = defineProps({
    carrito: {
        type: Array,
        required: true
    }
});

const emit = defineEmits(['eliminar-item', 'cerrar']);

const tallasDisponibles = ['S', 'M', 'L', 'XL'];

function calcularPrecioTotal() {
    let total = 0
    for (let i = 0; i < props.carrito.length; i++) {
        total += props.carrito[i].precioUnidad;
    }
    return total;
};

function obtenerProductosPorTalla(talla) {
    let listaFiltrada = [];
    for (let i = 0; i < props.carrito.length; i++) {
        if (props.carrito[i].talla === talla) {
            listaFiltrada.push(props.carrito[i]);
        }
    }
    return listaFiltrada;
};

function eliminarItem(item) {
    let indice = props.carrito.indexOf(item);
    emit('eliminar-item', indice);
};
</script>

<template>
    <div class="modal" @click.self="emit('cerrar')">
        <div class="contenido-modal">
            <div class="cabecera-carrito">
                <h2 class="titulo-seccion">Carrito de Compra</h2>
                <button @click="emit('cerrar')" class="btn-cerrar">Cerrar</button>
            </div>

            <div v-if="carrito.length === 0" class="carrito-vacio">
                El carrito está vacío.
            </div>

            <div v-else class="contenido-carrito">
                <div v-for="talla in tallasDisponibles" :key="talla">
                    <div v-if="obtenerProductosPorTalla(talla).length > 0" class="grupo-talla">
                        <h3 class="titulo-talla">Talla {{ talla }}</h3>
                        <ul class="lista-items">
                            <li v-for="(item, index) in obtenerProductosPorTalla(talla)" :key="index"
                                class="item-carrito">
                                <span class="info-item">
                                    <strong>{{ item.nombre }}</strong> - {{ item.precioUnidad }}€
                                </span>
                                <button @click="eliminarItem(item)" class="btn-eliminar">
                                    Eliminar
                                </button>
                            </li>
                        </ul>
                    </div>
                </div>

                <div class="resumen-total">
                    <strong>Precio final total: {{ calcularPrecioTotal() }}€</strong>
                </div>
            </div>
        </div>
    </div>
</template>

<style scope>
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
    box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2);
    width: 90%;
    max-width: 600px;
    max-height: 80vh;
    overflow-y: auto;
    color: #694F5D;
}

.cabecera-carrito {
    display: flex;
    justify-content: space-between;
    align-items: center;
    margin-bottom: 1em;
}

.titulo-seccion {
    margin: 0;
}

.btn-cerrar {
    background-color: #694F5D;
    color: white;
    border: none;
    padding: 6px 12px;
    border-radius: 0.3em;
    cursor: pointer;
}

.btn-cerrar:hover {
    background-color: #523d49;
}

.carrito-vacio {
    text-align: center;
    font-style: italic;
    padding: 1em 0;
}

.grupo-talla {
    background-color: #EFC7C2;
    border-radius: 0.5em;
    padding: 0.8em;
    margin-bottom: 1em;
}

.titulo-talla {
    margin: 0 0 0.5em 0;
    border-bottom: 1px solid #694F5D;
    padding-bottom: 0.2em;
}

.lista-items {
    list-style: none;
    padding-left: 0;
    margin: 0;
}

.item-carrito {
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 0.4em 0;
}

.btn-eliminar {
    background-color: #d9534f;
    color: white;
    border: none;
    padding: 4px 8px;
    border-radius: 0.3em;
    cursor: pointer;
}

.btn-eliminar:hover {
    background-color: #c9302c;
}

.resumen-total {
    font-size: 1.2em;
    text-align: right;
    margin-top: 1em;
    padding-top: 0.5em;
    border-top: 1px solid #694F5D;
}
</style>