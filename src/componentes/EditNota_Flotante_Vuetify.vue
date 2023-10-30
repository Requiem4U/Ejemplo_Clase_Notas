<template>
    <div class="text-center">
        <v-menu v-model="menu" :close-on-content-click="false" location="end">
            <template v-slot:activator="{ props }">
                <v-btn color="indigo" v-bind="props" append-icon="mdi-pencil-outline">
                    Editar
                </v-btn>
            </template>

            <v-card min-width="32vw" min-height="40vh">
                <h2>Editar Nota</h2>

                <v-divider></v-divider>

                <form>
                    <input v-model="nuevaInfo.titulo" placeholder="Título" required />
                    <textarea v-model="nuevaInfo.contenido" placeholder="Contenido" required
                        style="resize: none;"></textarea>
                </form>

                <v-card-actions>
                    <v-spacer></v-spacer>

                    <v-btn variant="text" @click="menu = false">
                        Cancelar
                    </v-btn>
                    <v-btn color="primary" variant="text" @click="guardar()">
                        Guardar
                    </v-btn>
                </v-card-actions>
            </v-card>
        </v-menu>
    </div>
</template>

<script setup>

import { defineProps, reactive } from 'vue';
import { ref } from 'vue';

let menu = ref(false)

const prop = defineProps(['nota'])
const emits = defineEmits(['guardarCambios', 'cerrar'])

let nuevaInfo = reactive({ ...prop.nota })

function guardar() {
    if (nuevaInfo.titulo != prop.nota.titulo || nuevaInfo.contenido != prop.nota.contenido) {
        emits('guardarCambios', nuevaInfo)
    }
    menu = false
}

function cerrar() {
    emits('cerrar');
}


</script>

<style scoped>
form {
    display: flex;
    flex-direction: column;
}

button {
    margin-top: 15px;
}

input,
textarea {
    width: 30vw;
    margin: 15px 10px 10px;
    padding: 8px;
    border: 1px solid #727171;
    box-shadow: 0 2px 4px rgba(153, 152, 152, 0.358);
}

input {
    height: 4vh;
}

textarea {
    height: 15vh;
}
</style>