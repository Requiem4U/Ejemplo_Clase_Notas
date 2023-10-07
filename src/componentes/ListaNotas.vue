<template>
    <div>
        <h2>Lista de Notas</h2>
        <div v-if="notas.length === 0">No hay notas.</div>
        <div v-else>
            <div v-for="(nota, index) in notas" :key="index" class="nota">
                <h3>{{ nota.titulo }}</h3>
                <p>{{ nota.contenido }}</p>
                <button @click="editar(index)">Editar</button>
                <button @click="eliminar(index)">Eliminar</button>
            </div>
        </div>

    </div>
</template>

<script setup>
import { defineProps } from 'vue';

const props = defineProps({
    notas: {
        type: Array,
        default: []
    }
})

const emits = defineEmits(['eliminarNota', 'editarNota'])

function editar(index) {
    const infoNota = { ...props.notas[index] };
    const nuevaInfo = {}
    nuevaInfo.titulo = prompt('Nuevo Título:', infoNota.titulo);
    nuevaInfo.contenido = prompt('Nuevo Contenido:', infoNota.contenido);

    if (nuevaInfo.titulo != null) {
        infoNota.titulo = nuevaInfo.titulo
    }
    if (nuevaInfo.contenido != null) {
        infoNota.contenido = nuevaInfo.contenido
    }

    emits('editarNota', index, infoNota);
}

function eliminar(index) {
    if (confirm('¿Estás seguro de eliminar esta nota?')) {
        emits('eliminarNota', index);
    }
}
</script>
  
<style scoped>
.nota {
    border: 1px solid #ccc;
    padding: 10px;
    margin: 10px 0;
}
</style>
  