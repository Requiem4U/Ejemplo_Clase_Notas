
<template>
  <div style="margin-top: 100px;">
    <h1>Aplicación de Notas</h1>
    <AgregarNota @nuevaNota="agregarNota" />
    <ListaNotas :notas="listaNotas" @editarNota="editarNota" 
    @eliminarNota="eliminarNota" />
  </div>

  <Ejmplo_Menu></Ejmplo_Menu>
  <EditNota_Flotante_Vuetify></EditNota_Flotante_Vuetify>

</template>

<script setup>
import ListaNotas from './componentes/ListaNotas.vue';
import AgregarNota from './componentes/AgregarNota.vue';
import Ejmplo_Menu from './componentes/Ejmplo_Menu.vue';
import EditNota_Flotante_Vuetify from './componentes/EditNota_Flotante_Vuetify.vue';

import { reactive } from 'vue';

let listaNotas = reactive([
  { titulo: 'Nota 1', contenido: 'Esta es la nota 1' },
  { titulo: 'Nota 2', contenido: 'Esta es la nota 2' },
  { titulo: 'Nota 3', contenido: 'Esta es la nota 3' },
])

function agregarNota(nuevaNota) {
  listaNotas.push(nuevaNota);
}

function editarNota(index, nuevaInfo) {
  listaNotas[index] = nuevaInfo
}
function eliminarNota(index) {
  listaNotas.splice(index, 1);
}

</script>

<style>
body {
  display: flex;
  justify-content: center;
  min-height: 100vh;
}

.lista {
  display: flex;
  flex-direction: column;
  font-family: Avenir, Helvetica, Arial, sans-serif;
}

h1,
h2 {
  text-align: center;
  margin-top: 20px;
}

*,
*::before,
*::after {
  margin: 0;
  position: relative;
  font-weight: normal;
}
</style>
