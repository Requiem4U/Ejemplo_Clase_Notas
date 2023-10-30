<template>
    <div>
        <h2>Lista de Notas</h2>
        <div v-if="notas.length === 0">No hay notas.</div>
        <div v-else>
            <div v-for="(nota, index) in notas" :key="index" class="nota">
                <h3>{{ nota.titulo }}</h3>
                <p>{{ nota.contenido }}</p>
                <button @click="mostrarEditarFlotante(nota)">Editar</button>
                <button @click="eliminar(index)">Eliminar</button>
            </div>
        </div>

        <EditarNota_Flotante v-if="notaEditando !== 0" :nota="notaEditando" 
        @guardar-cambios="guardarCambios"
            @cerrar="cerrarEditarFlotante"></EditarNota_Flotante>
    </div>
</template>

<script setup>
import EditarNota_Flotante from './EditarNota_Flotante.vue';
import { defineProps, ref } from 'vue';

const h = defineProps({
    notas: {
        type: Array,
        default: []
    }
})

const emits = defineEmits(['eliminarNota', 'editarNota'])

let notaEditando = ref(0)

function eliminar(index) {
    if (confirm('¿Estás seguro de eliminar esta nota?')) {
        emits('eliminarNota', index);
    }
}

function mostrarEditarFlotante(nota) {
    notaEditando.value = { ...nota };
}

function cerrarEditarFlotante() {
    notaEditando.value = 0;
}

const guardarCambios = (infoNota) => {
    const index = h.notas.findIndex(nota => nota.titulo === notaEditando.value.titulo);
    emits('editarNota', index, infoNota);
    cerrarEditarFlotante();
}
</script>
  
<style scoped>
.nota {
    border: 1px solid #ccc;
    padding: 10px;
    margin: 10px 0;
}
</style>
  