<template>
  <div>
    <h2>Agregar Nueva Nota</h2>
    <form @submit.prevent="agregar(this)">
      <input v-model="nuevaNota.titulo" placeholder="Título" required />
      <textarea v-model="nuevaNota.contenido" placeholder="Contenido" required 
      style="resize: none;"></textarea>
      <button type="submit">Guardar Nota</button>
    </form>
  </div>
</template>
  
<script setup>
import { reactive } from 'vue';

let nuevaNota = reactive({ titulo: '', contenido: '' })

function agregar(cntx) {
  cntx.$emit('nuevaNota', { ...nuevaNota });
  nuevaNota.titulo = '';
  nuevaNota.contenido = '';
}

</script>

<style scoped>
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

input{
  height: 4vh;
}

textarea{
  height: 15vh;
}
</style>
  