<script setup>
defineProps({
    cantidadCarrito: {
        type: Number,
        default: 0
    }
});

defineEmits(['abrir-modelos', 'abrir-carrito']);
</script>

<template>
    <header class="cabecera">
        <div class="top-bar">
            <h1 class="titulo-pagina">Camisetas Manu</h1>
            <h2 class="titulo2">Diseños y serigrafiado propios</h2>
        </div>
        <button @click="$emit('abrir-carrito')" class="btn-carrito">
            Carrito ({{ cantidadCarrito }})
        </button>

    </header>
</template>

<style scope>
.cabecera {
    max-width: 1100px;
    margin: auto;
    padding: 24px;
}

.titulo-pagina {
    color: #694F5D;
    font-family: Impact, Haettenschweiler, 'Arial Narrow Bold', sans-serif;
}

.titulo2 {
    color: #694F5D;
    font-family: 'Lucida Sans', 'Lucida Sans Regular', 'Lucida Grande', 'Lucida Sans Unicode', Geneva, Verdana, sans-serif;
}

.btn-carrito {
    background-color: #68A691;
    color: white;
    border: none;
    padding: 10px 16px;
    border-radius: 0.5em;
    font-weight: bold;
    cursor: pointer;
    margin: 10px;
}

.btn-carrito:hover {
    background-color: #558876;
}
</style>