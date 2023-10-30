<template>
    <div class="text-center">
        <v-select v-model="location" :items="locations" 
        label="Location"></v-select>
        <v-menu :location="location">
            <template v-slot:activator="{ props }">
                <v-btn color="primary" dark v-bind="props">
                    Dropdown
                </v-btn>
            </template>

            <v-list>
                <v-list-item v-for="(item, index) in items" :key="index">
                    <v-list-item-title>{{ item.title }}</v-list-item-title>
                </v-list-item>
            </v-list>
        </v-menu>
    </div>
</template>

<script setup>

import { ref, reactive } from 'vue';

let items = reactive([
    { title: 'Click Me' },
    { title: 'Click Me' },
    { title: 'Click Me' },
    { title: 'Click Me 2' },
])

let locations = reactive([
    'top',
    'bottom',
    'start',
    'end',
    'center',
])
let location = ref('end')
</script>