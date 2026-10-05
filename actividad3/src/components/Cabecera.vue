<script setup>
defineEmits(['abrir-modelos'])
</script>

<template>
    <header class="cabecera">
        <h1 class="titulo-pagina">Camisetas Manu</h1>
        <h2 class="titulo2">Diseños y serigrafiado propios</h2>
        <nav>
            <a href="#modelos">Modelos</a>
            <a href="#contacto">Contacto</a>
        </nav>
    </header>
</template>

<style scoped>
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

nav a {
    color: #694F5D;
    padding: 5px;
}
</style>