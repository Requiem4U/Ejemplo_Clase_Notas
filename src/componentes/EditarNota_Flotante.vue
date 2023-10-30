<!-- EditarNotaFlotante.vue -->
<template>
    <div class="editar-nota-flotante">
        <h2>Editar Nota</h2>
        <form @submit.prevent="guardar()">
            <input v-model="nuevaInfo.titulo" placeholder="Título" required />
            <textarea v-model="nuevaInfo.contenido" placeholder="Contenido" required style="resize: none;"></textarea>
            <div class="opcionesBoton">
                <button type="submit">Guardar Cambios</button>
                <button @click="cerrar()">Cancelar</button>
            </div>
        </form>
    </div>
</template>
  
<script setup>
import { defineProps, reactive } from 'vue';

const prop = defineProps(['nota'])
const emits = defineEmits(['guardarCambios', 'cerrar'])

let nuevaInfo = reactive({...prop.nota})

function guardar() {
    if(nuevaInfo.titulo!=prop.nota.titulo || nuevaInfo.contenido!=prop.nota.contenido){
        emits('guardarCambios', nuevaInfo);
    }
    cerrar();
}

function cerrar() {
    emits('cerrar');
}
</script>
  
<style scoped>
.editar-nota-flotante {
    display: flex;
    flex-direction: column;
    align-items: center;
    width: 32vw;
    height: 40vh;
    position: fixed;
    top: 50vh;
    left: 50vw;
    transform: translate(-50%, -50%);
    background-color: #fff;
    padding: 20px;
    border: 1px solid #727171;
    box-shadow: 0 2px 4px rgba(153, 152, 152, 0.358);
}

form {
    display: flex;
    flex-direction: column;
}

input,
textarea,
button {
    margin-top: 15px;
}

input,
textarea {
    width: 30vw;
}

input {
    height: 4vh;
}

textarea {
    height: 15vh;
}

button {
    width: 120px;
    height: 50px;
}

.opcionesBoton{
    display:  flex;
    justify-content: space-around;
}
</style>
  