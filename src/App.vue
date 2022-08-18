<script setup>
// creando una referencia reactiva
import {ref} from 'vue';

const header = ref("Lista de cursos");
const editing = ref(false);
const items = ref([
    {id : 1, label: 'Typescript'},
    {id : 2, label: 'Carbon'},
    {id : 3, label: 'Javascript'},
]);

const newItem =ref('');
const newItemPriority = ref(false);

// metodos
const saveItem = () => {
    items.value.push({id : items.value.length+1,label : newItem.value })
};
const toEdit = (edit) => {
    editing.value = edit
}

</script>

<template>
<div class="tareas container">

    <div class="task__contenedor">
          <h2 class="heading">{{header}}</h2>
          <!-- boton cancelar -->
          <button class="bton cancelar" v-if="editing" @click="toEdit(false)">
            Cancelar
          </button>
          <!-- botn agregar -->
          <button v-else class="bton aceptar" @click="toEdit(true)">
            Agregar Tarea
          </button>
    </div>

    <!-- container form -->
    <div class="form" v-if="editing">
        <div class="campo">
            <input 
            @keyup.enter="saveItem"
            type="text" 
            v-model="newItem"
            >

            <button 
            class="bton campo__agrega" 
            @click="saveItem">
              Agregar
            </button>
        </div>
        <div class="prioridad">
            <strong class="strong">Nivel de prioridad</strong>
            <input type="checkbox" v-model="newItemPriority"/>
        </div>
    </div>
    
    <!-- condicional -->
    <p v-if="items.length === 0" class="no-hay">No hay tareas</p>

    <!-- renderizar listas -->
    <ul>
        <li v-for="{label, id} in items" :key="id">
            <p class="item__parrafo">{{label}}</p>
        </li>
    </ul>

</div>
</template>

